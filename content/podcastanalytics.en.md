Title: Podcast Analytics
Date: 20.05.2021, 11:36
Type: page
Permalink: /podcastanalytics-en/

## Podlove-Stats for on the go

You're running a podcast-show and use Wordpress and the [Podlove Publisher](https://publisher.podlove.org/) to publish it? But you don't want to login every time when you want to have a glimpse at the stats? What about an App for iPhone and iPad? Say “hello” to Podcast Analytics!

# Hello!

![](PA_Dark_EN.jpeg)

# Features

- Shows the download numbers of your podcast hosted with Podlove on your iPhone or iPad.
- You can see them either in a table or in an interactive chart.
- That's it.

![](PA_Light_EN.jpeg)

# Download

[![](Download_on_the_App_Store.png)](https://itunes.apple.com/us/app/podcast-analytics/id1460023828?l=de&ls=1&mt=8)

# Requirements

In order to use the app, you must run a set of certain software on your server. This is a pretty popular setup among podcasters in Germany, who don't use a paid service.

- **Wordpress**: Please make sure to run [Wordpress](https://wordpress.org) version `4.4` (or higher). Also, the login-page `wp-login.php` needs to be accessible. Otherwise, you can use an Authentication-plugin (see below).
- **Podlove Podcast Publisher**: You also need the [Podlove Podcast Publisher-plugin](https://publisher.podlove.org) for Wordpress, at least version `2.7.17` (or higher)). You have to enable the Podlove-analytics. Otherwise, the app wouldn't make a lot of sense for you
- **HTTPS**: Your server must have a valid SSL-certificate. If you don't have one yet, you might want to have a look at [Let's Encrypt](https://letsencrypt.org).
- **User Account**: Please note, that you need a Wordpress user account, that also can access the Podlove stats on the website. According to the [Release Notes of the Podlove Publisher](https://wordpress.org/plugins/podlove-podcasting-plugin-for-wordpress/#developers) this user account must have the `podlove_read_analytics`-permission. This means, that the user account must be one of the following roles on an unmodified Wordpress-installation: "author", "editor", or "admin".
- A **Wordpress-Auth-Plugin (Optional)**: If you prefer to use an [Authentication-plugin](https://developer.wordpress.org/rest-api/using-the-rest-api/authentication/#authentication-plugins) for your Wordpress, just install one and use the credentials from this plugin to login. Podcast Analytics has been tested and used with [Application Passwords](https://wordpress.org/plugins/application-passwords/) and, for development purposes, with [Basic-Auth](https://github.com/WP-API/Basic-Auth). In older versions of the app (prior to `2021.1`) this plugin was mandatory.


# Questions? Feedback?

You have something important to say? Maybe valuable feedback or feature requests? Or you just want to be a beta-tester? I'm really looking forward to hearing from you! Just send me an [e-mail to podcast-app(at)bullenscheisse.de](mailto:podcast-app@bullenscheisse.de) or a direct message on either [Twitter](https://twitter.com/zeitschlag) or [Mastodon](https://chaos.social/@zeitschlag).
