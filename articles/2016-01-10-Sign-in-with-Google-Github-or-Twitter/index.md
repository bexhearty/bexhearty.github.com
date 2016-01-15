# Sign in with Google, Github, or Twitter
When you should or shouldn't

The joys of password creation! Some sites require passwords with at least 6 characters, others require at least one number and a character (but make sure that the character is not a \ ), others require you to have both a capital and a lower case letter... and make sure that the capital letter is not at the begining or at the end of the password. Oh, also make sure your password is unique to the site, and that you change it often. 

![](http://i.imgur.com/fUMJpI1.png)


Inevitably, we all end up creating just one password. One really good password, you know, something like `pAssw0rd!` and then use that REALLY good password for every site. And never change it. 

One problem with this technique is that if a site's database is compromised, access to all other sites is compromised. We’ve heard that a thousand times already, however, and to most of us, the risk outweighs the annoyance. Note: If you click on "Forgot password" on any site and get an email with your actual password, run away from that service - your data is being handled by amateurs. If the site is able to send an email with the password you created, it means that the site is either saving your password in plain text, or is storing a simple encryption of your password. 

Storing plaintext or encrypted passwords with a simple key are the easiest methods for developers to handle passwords, and also the easiest to access by an attacker. A safer way for sites to deal with passwords is by using a salted version of the [hashed password](https://crackstation.net/hashing-security.htm) or by using an encryption algorithm such as [bcryt](http://bcrypt.sourceforge.net/) both of which are more involved processes from the developer standpoint. The safest way for sites to deal with passwords is to not deal with passwords at all. 

If you use your one really good password on every site, you will be better off logging in with either Google, Github, Twitter or any other site that offers a login service--in particular if your really good password is what you also use to login into any of those sites. The service is called oAuth. oAuth exchanges security keys between the new site and Google, Github or Twitter and they handle the logging without involving the creation of new passwords. Sometimes the new sites will ask your permission to export into their site additional data from Google, usually, your email address and avatar. Some more creepy services ask for permission to access your contacts, demographic and geographic data, and others ask your permission to actually act on your behalf into the service (i.e. Tweet for you). 

Initially, you may be confused why Google, Github, or Twitter would offer a free service to handle logins through oAuth. Altruism? One motivation is to leverage as many services as possible to your account in order to reduce the chances of you churning and closing that account. For Google, the motivation might be more geared towards tracking which apps you use and how often. A newer and more interesting oAuth service provider is the banking industry. Now you can use your American Express login credentials to sign up to AirBnb, granting AirBnb access some data from your Amex account. When using oAuth is always important to check what data access or permissions you are granting to the new site.

![](http://i.imgur.com/LxgZ0Ry.png)

Unless the new site is asking for too much data, for me, the benefits from oAuth almost always outweighs the risk of compromising my REALLY good password. Even if that means granting access to additional basic data points so that Google can have a clearer picture of "Who you are to Google."

To review the list of authorized applications on each of your accounts go to: [Google](https://security.google.com/settings/security/permissions), [Github](https://help.github.com/articles/keeping-your-ssh-keys-and-application-access-tokens-safe/#reviewing-your-authorized-applications-oauth), and [Twitter](https://twitter.com/settings/applications).

Coming next: Who you are to Google 