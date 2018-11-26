# Crontab commands

Edit user crontab file

```
sudo rontab -e
```

Basic commands, sometimes you should reset the service

```
service crond status
service crond start
service crond stop
```

Also the mail can be added, each time it works the result will be sent. Be carrefoul with that obviosly if you run something every minute...

```
MAILTO="info@example.org"
```