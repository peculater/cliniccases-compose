# ClinicCases in docker compose

## Run ClinicCases

* docker-compose up

* Head to [http://localhost:8000/_INSTALL](http://localhost:8000/_INSTALL)

* Fill out the form, these values are also specified in `_CONFIG.php`

```
Host: mysql
Database Username: cliniccases
Database Password: terriblepassword
Database Name: cliccases
Password Salt (leave alone)
Path to ClinicCases: /var/www/html
Path to Documents: /var/cc_docs
Base URL: http://localhost:8000/
Domain: http://localhost:8000
Admin Email: cliniccases@example.com
Default Email: cliniccases@example.com
(Everything underneath that is fine)
```

* Click Submit

* Head to [http://localhost:8000](http://localhost:8000)

* Log in with admin:admin

## Other notes

Mail doesn't work so creating users is a little more complex.  You have to create them, then reset their password to see what the password got set to.

Otherwise, things seem to work ok. 

If this goes to prod, we'll want to make a container that doesn't have _INSTALL up ins.



