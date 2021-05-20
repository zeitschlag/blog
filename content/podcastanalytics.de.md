Title: Podcast Analytics
Date: 20.05.2021, 11:36
Type: page
Permalink: /podcastanalytics/

## Podlove Analytics für unterwegs

Du produzierst einen Podcast, nutzt Wordpress und den [Podlove Publisher](https://publisher.podlove.org/) und willst dich nicht immer einloggen, um einen Blick auf Deine Downloadzahlen zu werfen? Wie wär's mit einer App für Dein iPhone und iPad? Sag „Hi“ zu Podcast Analytics!

# Hi!

![](PA_Dark_DE.jpeg)

# Features

- Anzeige der Downloadzahlen für deinen Podcast auf deinem iPhone oder iPad
- Es gibt eine Tabelle, einen Dark Mode und ein interaktives Diagramm
- Das war's.

![](PA_Light_DE.jpeg)

# Her damit

[![](Download_on_the_App_Store.png)](https://itunes.apple.com/de/app/podcast-analytics/id1460023828?l=de&ls=1&mt=8)

# Voraussetzungen

Damit du die App überhaupt und sinnvoll nutzen kannst, musst du bestimmte Software auf deinem Server einsetzen.

- **Wordpress**: Bitte achte darauf, dass [Wordpress](https://wordpress.org) in der Version `4.4` (oder neuer) installiert ist. Ausserdem muss Deine Login-Seite `wp-login.php` erreichbar sein. Wenn sie das beispielsweise aus Sicherheitsgründen nicht ist, musst du dir ein Authentifizierungsplugin installieren (siehe unten) 
- **Podlove Podcast Publisher**: Neben Wordpress brauchst du auch noch das Wordpress-Plugin [Podlove Podcast Publisher](https://publisher.podlove.org) in der Version `2.7.17` (oder neuer). Es wäre sinnvoll, wenn du die Podlove-Analytics aktiviert hast, denn sonst ergibt diese App für dich relativ wenig Sinn.
- **HTTPS**: Dein Server muss über ein gültiges SSL-Zertifikat verfügen. Wenn du das noch nicht hast, wird es auch unabhängig von dieser App höchste Zeit. Schau mal bei [Let's Encrypt](https://letsencrypt.org) vorbei.
- **Benutzeraccount**: Bitte beachte, dass du für die App einen Benutzeraccount benötigst, mit dem du auch im Podlove Publisher die Statistiken betrachten kannst. Dieser Benutzeraccount muss bei einer unveränderten Standardinstallation von Wordpress die Rolle „Autor“, „Redakteur“ oder „Administrator“ innehaben. Laut den [Release Notes des Podlove Publishers](https://wordpress.org/plugins/podlove-podcasting-plugin-for-wordpress/#developers) muss dein Benutzeraccount die `podlove_read_analytics`-Rechte besitzen.
- **Wordpress-Auth-Plugin (Optional)**: Du musst dich nicht mit deinen Wordpress-Zugangsdaten anmelden, du kannst stattdessen auch ein [Authentifizierungsplugin](https://developer.wordpress.org/rest-api/using-the-rest-api/authentication/#authentication-plugins) nutzen. Die App wurde bisher mit [Application Passwords](https://wordpress.org/plugins/application-passwords/) und testweise mit [Basic-Auth](https://github.com/WP-API/Basic-Auth) verwendet. In älteren Versionen der App (vor `2021.1`) war ein solches Plugin zwingend erforderlich.


# Fragen? Feedback? Wünsche?

Du willst deinen Senf dazugeben? Hast Verbessungsvorschläge und Wünsche? Willst an einer Beta teilnehmen? Ich freue mich darauf, von dir zu hören! Schreib mir gerne eine [Email an podcast-app(at)bullenscheisse.de](mailto:podcast-app@bullenscheisse.de) oder eine Direktnachricht auf [Twitter](https://twitter.com/zeitschlag) oder [Mastodon](https://chaos.social/@zeitschlag).
