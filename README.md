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

Et voila - enyoy playing DnD on your server!

## Backstory

Back in 2020 during pandemic, my firends and I started playing DnD. One friend bought foundryvtt licence and I had a server doing nothing.
Now their documentation did not even mention systemd back then. So I had to write the file and do the setup myself.

If you find any error or have an improvement in mind, feel free to submit a PR 😃
