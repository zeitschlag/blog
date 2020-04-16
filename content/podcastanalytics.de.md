Title: Podcast Analytics-App
Date: 15.04.2020, 08:59
Type: page
Permalink: /podcastanalytics/

## Podlove Analytics für unterwegs

![](PA_Screenshots.jpeg)

# Features

- Anzeige der Downloadzahlen für deinen Podcast auf deinem iPhone oder iPad
- Es gibt eine Tabelle und ein interaktives Diagramm
- Das war's.

# Her damit

[![](Download_on_the_App_Store.png)](https://itunes.apple.com/us/app/podcast-analytics/id1460023828?l=de&ls=1&mt=8)

# Voraussetzungen

Damit du die App überhaupt und sinnvoll nutzen kannst, musst du bestimmte Software auf deinem Server einsetzen.

- **Wordpress**: Bitte achte darauf, dass [Wordpress](https://wordpress.org) in der Version `4.4` (oder neuer) installiert ist. 
- **Podlove Podcast Publisher**: Neben Wordpress brauchst du auch noch das Wordpress-Plugin [Podlove Podcast Publisher](https://publisher.podlove.org) in der Version `2.7.17` (oder neuer). Es wäre sinnvoll, wenn du die Podlove-Analytics aktiviert hast, denn sonst ergibt diese App für dich relativ wenig Sinn.
- **Wordpress-Auth-Plugin**: Zu guter Letzt benötigst du noch ein [Authentifizierungsplugin](https://developer.wordpress.org/rest-api/using-the-rest-api/authentication/#authentication-plugins), damit die App sich bei deiner Wordpress-Installation einloggen kannst. Die App wurde bisher mit [Application Passwords](https://wordpress.org/plugins/application-passwords/) und testweise mit [Basic-Auth](https://github.com/WP-API/Basic-Auth) verwendet.
- **HTTPS**: Dein Server muss über ein gültiges SSL-Zertifikat verfügen. Wenn du das noch nicht hast, wird es auch unabhängig von dieser App höchste Zeit. Schau mal bei [Let's Encrypt](https://letsencrypt.org) vorbei.
- **Benutzeraccount**: Bitte beachte, dass du für die App einen Benutzeraccount benötigst, mit dem du auch im Podlove Publisher die Statistiken betrachten kannst. Dieser Benutzeraccount muss bei einer unveränderten Standardinstallation von Wordpress die Rolle „Autor“, „Redakteur“ oder „Administrator“ innehaben. Laut den [Release Notes des Podlove Publishers](https://wordpress.org/plugins/podlove-podcasting-plugin-for-wordpress/#developers) muss dein Benutzeraccount die `podlove_read_analytics`-Rechte besitzen.

# Fragen? Feedback? Wünsche?

Du willst deinen Senf dazugeben? Hast Verbessungsvorschläge und Wünsche? Willst an einer Beta teilnehmen? Ich freue mich darauf, von dir zu hören! Schreib mir gerne eine [Email an podcast-app(at)bullenscheisse.de](mailto:podcast-app@bullenscheisse.de) oder eine Direktnachricht auf [Twitter](https://twitter.com/zeitschlag) oder [Mastodon](https://chaos.social/@zeitschlag).
