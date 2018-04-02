# Matomo setup

See the [official site](https://matomo.org/) to get more information about Matomo, formerly known as Piwik.

## On the remote server

Clone this repository, fill place holders with your passwords of choice and start MySQL (will run on port 3306) and Matomo web application (will run on port 8085).

```
cp ./docker-compose.yml.template ./docker-compose.yml
sed -i 's/<root_passwd>/yourRootPasswd/g' ./docker-compose.yml
sed -i 's/<piwik_passwd>/yourPiwikPasswd/g' ./docker-compose.yml
docker-compose up
```

## Local port forwarding on local machine

Add these lines to .ssh/config to enable port forwarding:

```
Host kiesinger
    HostName kiesinger.okfn.de
    Port 2201
    User joerg
    LocalForward 3006 localhost:3306
    LocalForward 8085 localhost:8085
```

In terminal open connection to remote server: `ssh kiesinger`

Open localhost:8085 in browser.

## Configure matomo

Follow the configuration dialog as described [here](https://matomo.org/docs/installation/#the-5-minute-matomo-installation),
except that using "mysql" in field "database server" instead of "localhost" in the third step.

Store the credentials you come up with in step 6 somewhere where don't lose it (e.g. in a password store like Keepass).

The setup after last step may take some time so reload localhost:8085 in browser until a login page appears where you
can login with the credentials you stated in step 6 ("Super user") before.

Navigate to "Administration" button (third icon from right in toolbar) and then in the left navigation bar to "Web sites",
"Manage" resp. "Verwalten". Here you can configure existing and add new Web sites to track. Under "Web sites" / "Tracking code"
you can configure and copy the Javascript you have to include later in the web site to track.

Instead of including the Javascript code manually you may use existing Matomo/Piwik integrations for your web frameworks, e.g.:
 * [Django](https://gitlab.com/burke-software/django-server-side-piwik)
 * [Rails](https://matomo.org/blog/2012/10/integrate-piwik-into-your-rails-application/)
 * [Angular](https://github.com/mike-spainhower/angular-piwik)

See [integrations](https://matomo.org/integrate/) for a complete list, but be aware, that some plugins might not be actively maintained anymore.


