# foundryvtt-systemd
Systemd files and howto for foundryvtt

## General information

This repository contains systemd file and documentation for running [Foundry Virtual Tabletop](https://foundryvtt.com/) as Linux systemd service.

## Systemd how to

When needed, consult official installation guide! [https://foundryvtt.com/article/installation/](https://foundryvtt.com/article/installation/)

### Step by step

1. Create foundryvtt user `useradd -m foundryvtt`
2. Create directory structure `mkdir /opt/foundryvtt /opt/foundryvttdata`
3. Download foundry zip and uzip contents to `/opt/foundryvtt`
4. Install nodejs (follow official guide or even better official documentation of your Linux server distribution)
5. Give foundryvtt user rights over the directories `chown -R foundryvtt:foundryvtt /opt/foundryvtt; chown -R foundryvtt:foundryvtt /opt/foundryvttdata`
6. Copy `foundryvtt.service` from this project to `/etc/systemd/system/`
7. Run `systemctl enable foundryvtt.service; systemctl start foundryvtt.service` <- This will enure that foundry is started when you start/restart the server
8. Check the following url <your server ip>:30000 and verify that foundry is installed.

Et voilà - enyoy playing DnD on your server!

### Tips for nginx

I used nginx as proxy so that foundry would run on / of server. No need to go through :30000 port.
Following is only snippet, do not replace server nginx.config with the following. Adapt it and copy where it suits you.

```nginx
...

http {
  # Add following directives to increase upload size through the foundy application when using nginx
  # Otherwise our dungeon master had problem uploading images and assets due to some ridiculously low upload size limit
  include       mime.types;
  default_type  application/octet-stream;
  client_max_body_size 50M;

  ...

  # Something like this should ensure that any request to / will be passed to our application running on :30000
  server {
    location / {
      proxy_pass http://localhost:30000;
      proxy_http_version 1.1;
      proxy_set_header Upgrade $http_upgrade;
      proxy_set_header Connection 'upgrade';
      proxy_set_header Host $host;
      proxy_cache_bypass $http_upgrade;
    }
  }
  ...
}
```

## Backstory

Back in 2020 during pandemic, my firends and I started playing DnD. One friend bought foundryvtt licence and I had a server doing nothing.
Now their documentation did not even mention systemd back then. So I had to write the file and do the setup myself.

If you find any error or have an improvement in mind, feel free to submit a PR 😃
