Title: pretix auf einem Uberspace
Tags: [#pretix, #uberspace]
Date: 23.03.2018, 13:21

Im Oktober 2015 schrieb ich eine [Anleitung](/2015/pretix-auf-einem-uberspace-installieren/), wie man [pretix](https://github.com/pretix/pretix) auf einem [Uberspace](https://uberspace.de) installiert. Nun ist heute nicht mehr Oktober 2015 und die alte Anleitung entsprechend nicht mehr aktuell. Mich haben mehrere Leute darauf hingewiesen. Ausserdem brauche ich aus [Gründen](/2018/osstatus-com/) selbst ab und an mal eine pretix-Instanz und habe mich entschlossen, die Anleitung mal zu überarbeiten und in diesem Blogpost auf einen neueren Stand zu bringen.

## Einleitung

pretix ist ein Stück freie Software, mit dem man Tickets für Konzerte, Messen, Barcamps und sonstige Veranstaltungen verkaufen kann. Das Tool setzt auf [Django](https://www.djangoproject.com) und benötigt Python 3. 

Es lässt sich unter [Linux](https://docs.pretix.eu/en/latest/admin/installation/manual_smallscale.html) installieren, die Anleitung dafür kann man aber nicht eins zu eins auf die Ubernauten übertragen. Im Folgenden möchte ich beschreiben, was ich tun musste, um pretix auf einem Uberspace zumindest zum Laufen zu bringen. Der Benutzername für den Uberspace ist `barcamp`, der Uberspace selbst heisst `kaul`. Ich möchte noch darauf hinweisen, dass diese Installation eine SQLite-Datenbank nutzt. Die Dokumentation sagt dazu:

> If you have real users on your system you’ll really want to use
>
> A database (MySQL or PostgreSQL)
>
> A reverse proxy web server (nginx or Apache)

Die Datenbank ist dieser Anleitung egal. Ausserdem fehlen noch ein, zwei andere Kleinigkeiten (siehe unten), um so Sachen wie SSL musst du dich ebenfalls selbst kümmern. Im Großen und Ganzen habe ich mich an die Anleitung der Ubernauten für [Django](https://wiki.uberspace.de/cool:django) gehalten und sie mit besagter Installationsanleitung für Linux gekreuzt. 

Trotzdem gilt: Du wirst diese Anleitung nicht in dieser Form übernehmen können. **Lies sie aufmerksam und benutze deinen eigenen Kopf, um Anpassungen zu machen** Wenn du irgendwo nicht weiterkommst oder eine Anregung hast, dann freue ich mich natürlich über [Fragen und Feedback](/about/).

Wenn du — warum auch immer — keine eigene pretix-Instanz betreiben möchtest, kannst du ja mal darüber nachdenken, die gehostete Version zu nutzen. Raphael bietet die Software auch as a Service an — zu [sehr erschwinglichen Konditionen](https://pretix.eu/about/de/pricing).

## Anleitung

### pretix-Installation an sich

In einem erste Schritt lege ich einen Ordner für die eigentliche pretix-Installation, die Virtual Environment und das Verzeichnis für die pretix-Daten an:

    [barcamp@kaus ~]$ mkdir pretix_installation
    [barcamp@kaus ~]$ cd pretix_installation

Anschließend richte ich die [virtuelle Umgebung](https://virtualenv.pypa.io/en/stable/) mit Python 3.6 ein und aktiviere sie:

    [barcamp@kaus pretix_installation]$ python3.6 -m venv env
    [barcamp@kaus pretix_installation]$ source env/bin/activate

Zwar gibt es pretix auch im [Python Package Index](https://de.wikipedia.org/wiki/Pip_(Python)), aber weil ich ein paar Uberspace-spezifische Anpassungen in der `settings.py` vornehmen muss, bringt das — zumindest nach meinem Kenntnisstand, vielleicht weißt du es besser, dann lass mich bitte an deinem Wissen teilhaben — wenig. Zeit, das entsprechende Repository auf Github zu klonen und in den Ordner zu wechseln:

    (env) [barcamp@kaus pretix_installation]$ git clone https://github.com/pretix/pretix.git
    (env) [barcamp@kaus pretix_installation]$ cd pretix

Wenn du ein spezielles Release möchtest, wäre jetzt der richtige Zeitpunkt, den entsprechenden Branch oder Tag auszuchecken. Ich gehe davon aus, dass das Repository in einem Ordner namens `~/pretix_installation/pretix` liegt. Nun geht es daran, die Abhängigkeiten von pretix zu installieren:

    (env) [barcamp@kaus pretix]$ pip install -U gunicorn
    (env) [barcamp@kaus pretix]$ pip install -U -r src/requirements.txt

Danach muss ich — wie bereits erwähnt — die `settings.py` erweitern, wie bei den Ubernauten beschrieben:

    (env) [barcamp@kaus pretix]$ cat << __EOF__ >> src/pretix/settings.py
    
    USE_X_FORWARDED_HOST = True
    
    __EOF__

Wie ebenfalls oben bereits erwähnt, braucht pretix ein Ordner, in dem es alle möglichen Daten ablegen kann. In diesem Beispiel ist es unter anderem die SQLite-Datenbank.

    (env) [barcamp@kaus pretix]$ mkdir ../data_dir

pretix schaut an einigen Stellen nach der benötigten [Konfigurationsdatei](https://docs.pretix.eu/en/latest/admin/config.html), unter anderem im Home-Verzeichnis. Aus Bequemlichkeitsgründen lege ich sie deshalb einfach mal da an:

    (env) [barcamp@kaus pretix]$ cat << __EOF__ > ~/.pretix.cfg
    
    [pretix]
    instance_name=Frische Tickets!
    url=https://pretix.barcamp.kaus.uberspace.de
    currency=EUR
    datadir=/home/barcamp/pretix_installation/data_dir
    
    [database]
    ; Replace mysql with postgresql_psycopg2 for PostgreSQL
    backend=sqlite3
    
    __EOF__

Wahrscheinlich — hoffentlich — wird deine anders aussehen. In der Konfigurationsdatei stehen alle möglichen Informationen, abhängig davon, was du alles nutzen möchtest. Beispielsweise steht hier die URL, unter der pretix erreichbar ist oder auch, wo sich das Verzeichnis für die Daten befindet.

Hier sei nochmal ein Blick in die entsprechende [Dokumentation](https://docs.pretix.eu/en/latest/admin/config.html) von pretix empfohlen — sie ist sehr gut. Danach initialisiere ich die Datenbank und lasse die statischen Dateien erstellen. Das hat mir bei etwas gedauert:

    (env) [barcamp@kaus pretix]$ python src/manage.py migrate
    (env) [barcamp@kaus pretix]$ python src/manage.py rebuild
    (env) [barcamp@kaus pretix]$ deactivate

Damit bin ich mit der Installation von pretix durch.

### Deamon und Erreichbarkeit

Ich könnte pretix jetzt wie jede andere Django-Anwendung starten. Es würde jedoch nicht im Hintergrund laufen und wäre noch nicht aus dem Internet erreichbar. Darum kümmere ich mich jetzt. Zuerst brauche ich dafür einen Port. Die [Ubernauten empfehlen folgenden Weg](https://wiki.uberspace.de/cool:django#deamon_einrichten), den ich einfach mal guttenberge:

    [barcamp@kaus ~]$ DJANGOPORT=$(( $RANDOM % 4535 + 61000)); netstat -tulpen | grep $DJANGOPORT && echo "versuch's nochmal"

>  wenn hier keine Ausgabe `versuch's nochmal` erscheint, passt alles. Wenn `versuch's nochmal` kommt - versuchs noch mal :)

Danach richte ich den eigentlichen Service ein, der sich darum kümmert, dass pretix im Hintergrund läuft:

    [barcamp@kaus ~]$ test -d ~/service || uberspace-setup-svscan 
    [barcamp@kaus ~]$ uberspace-setup-service pretix /home/barcamp/pretix_installation/env/bin/gunicorn --error-logfile ~/error-log --reload --chdir /home/barcamp/pretix_installation/pretix/src --bind 127.0.0.1:$DJANGOPORT --workers 4 pretix.wsgi --name pretix --max-requests 1200 --max-requests-jitter 50

Im letzten Schritt muss ich dafür sorgen, dass dieser Service aus dem Internet ansprechbar ist:

    [barcamp@kaus ~]$ mkdir /var/www/virtual/barcamp/barcamp.kaus.uberspace.de
    [barcamp@kaus ~]$ cat << __EOF__ > /var/www/virtual/barcamp/pretix.barcamp.kaus.uberspace.de/.htaccess
    RewriteEngine On
    RewriteCond %{REQUEST_FILENAME} !-f
    RewriteBase /
    RewriteRule ^(.*)$ http://127.0.0.1:$DJANGOPORT/$1 [P]
 
    RequestHeader set X-Forwarded-Proto https env=HTTPS
    __EOF__

Das war's.

### Läuft bei mir

pretix wäre bei mir jetzt unter [https://pretix.barcamp.kaus.uberspace.de](https://pretix.barcamp.kaus.uberspace.de) erreichbar.

![Startbildschirm von pretix](/img/IMG_132_pretix.png)

 Da sieht man denn natürlich nicht viel, weswegen ich mich unter `http://pretix.barcamp.kaus.uberspace.de/control/login?next=/control/` anmelden kann. Als Benutzername habe ich `admin@localhost`, als Passwort `admin` verwendet. **Bitte denk daran, die Anmeldedaten zu ändern!**
 
![Anmeldebildschirm von pretix](/img/IMG_99.png)

## Was noch fehlt

### Domain

Wie dir vielleicht aufgefallen ist, läuft pretix unter einer Subdomain — apropos Domain: [pretix.barcamp.kaus.uberspace.de](https://pretix.barcamp.kaus.uberspace.de) ist wesentlich weniger lesbar als beispielsweise [pretix.domain.tld](https://pretix.domain.tld), du willst vielleicht also eine [Domain](https://wiki.uberspace.de/domain) haben.

Ich habe es zwischendrin mal hinbekommen, dass pretix auch in einem Unterordner lief, mir aber nicht aufgeschrieben, wie es geklappt hat und nun kann ich als Django/Python-Amateur das nicht mehr nachvollziehen. Falls jemand einen Hinweis hat, bin ich dankbar.

### pretix-worker, Mails, MariaDB, Plugins...

Was ebenfalls nicht läuft, ist der in der pretix-Dokumentation erwähnte *pretix-worker*, ebenfalls fehlen sämtliche — bisweilen obligatorische — Zusatzssachen wie Mail, eine ordentliche Datenbank, *redis*, HTTPS, Plugins... Kurz: Sieh diese Anleitung bitte als einen ersten Schritt und kümmere dich anschliessend selbst darum, dass deine pretix-Installation gut und sicher läuft. Danke.

## Links

- [pretix im Netz](https://pretix.eu/about/de/)
- [pretix auf Github](https://github.com/pretix/pretix)
- [pretix-Dokumentation](https://docs.pretix.eu/en/latest/)
