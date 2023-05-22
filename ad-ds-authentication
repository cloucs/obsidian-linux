hostname anpassen
$ sudo vim /etc/hosts
$ sudo hostnamectl set-hostname "client.domain.org"
$ sudo hostnamectl
$ hostname -f

dns eintragen/überprüfen
$ sudo vim /etc/resolv.conf

pakete installieren
$ sudo apt -y install realmd libnss-sss libpam-sss sssd-tools adcli samba-common-bin oddjob oddjob-mkhomedir packagekit

in domäne aufnehmen
$ sudo realm discover hotel-hamburg-zentrum.de
$ sudo realm join hotel-hamburg-zentrum.de
$ sudo realm join -v hotel-hamburg-zentrum.de
$ sudo realm list

einstellungen anpassen/überprüfen
$ sudo vim /etc/sssd/sssd.conf

automatische homedir erstellung aktivieren
$ sudo pam-auth-update --enable mkhomedir

userdaten überprüfen
$ sudo getent passwd "vor.nachname@domain.org"
$ sudo login

neustart
$ sudo reboot now
