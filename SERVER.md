# Development aplikacji

<br>

## 1. Zakładamy konto np. na [digitalocean](https://digitalocean.com)

Ustawiamy hasło do root.

<br>

Wklejamy publiczny klucz z naszego koputera na serwer.

```
ssh-copy-id root@46.41.143.70
```

Lub kopiujemy klucz publiczny SSH Key do clipbordu za pomocą kodu i wklejamy w panelu klienta.

```
pbcopy < ~/.ssh/id_rsa.pub
```

<br><br>

## 2. Łączymy się z serwerem

```
 ssh root@46.41.143.70
```

Przy pierwszym logowaniu wpisujemy hasło.

<br><br>

## 3. Uaktualnienie serwera

Sprawdzamy czy mamy apacha

```
which apache2
whereis apache2
systemctl status apache2
```

Deleting apache server

```
systemctl stop apache2
```

```
systemctl disable apache2
```

```
apt remove apache2
```

---

<br><br>

Used to clear disk space as needed, generally as part of regularly scheduled maintenance.

```
apt clean
```

Update server components list with

```
apt update
```

Upgrade server components with

```
apt dist-upgrade
```

it will install everything required for compiling

```
apt install build-essential
```

delete related dependencies:

```
apt autoremove
```

Restart serwera

```
reboot now
```

---

Można łączyć komendy

```
apt clean && sudo apt update && sudo apt dist-upgrade
```

<br><br>

## 4. Instalacja Node.js

Checking your version of npm and Node.js

```
node -v
npm -v
```

Instalacja [NVM - node version menager](https://github.com/nvm-sh/nvm)

```
apt install curl
curl -sL https://deb.nodesource.com/setup_14.x | sudo -E bash -
apt install nodejs
```

Lub

```
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.38.0/install.sh | bash
nvm install node
```

Uaktualnienie wersji npm

```
npm install npm@latest -g
```

<br><br>

## 5. Instalacja Nginx (HTTP Server)

```
apt install nginx
```

Uruchomienie po reboocie serwera

```
systemctl enable nginx
```

Sprawdzamy czy został uaktywniony

```
systemctl status nginx
```

<br><br>

## 6. Instalacja PM2

```
npm install pm2@latest -g
```

Uruchamianie aplikacji

```
pm2 start app (or whatever your file name)
```

Nadanie nazwy procesowi

```
pm2 start server.js --name nazwa-procesu
```

Other pm2 commands

```
pm2 show app
pm2 status
pm2 restart app
pm2 stop app
pm2 logs (Show log stream)
pm2 flush (Clear logs)
```

To make sure app starts when reboot

```
pm2 startup ubuntu
```

<br><br>

## 7. Instalacja GIT

```
apt install git
git --version
```

<br><br>

## 8. Instalacja Firewall

To view firewall status

```
ufw status
```

Install Firewall - jeśli nie jest zainstalowany

```
apt install ufw
```

Enable Ports on Firewall

```
ufw allow ssh
ufw allow http
ufw allow https

or

sudo ufw allow 'OpenSSH'
sudo ufw allow 'Nginx Full'
```

Enable Firewall

```
ufw enable
```

To view firewall status

```
ufw status
ufw app list
```

Jeśli mamy problemy z kernelem to wyłączamy logi:

```
ufw logging off
```

Uninstall Firewalla

```
apt remove ufw
```

<br><br>

## 8. Podłączenie domen, subdomen

Dodajemy nowe rekordy do domeny w panelu klienta

```
Type: A Record
Host: www
Value: adrei IP

dodatkowy rekord - niezawsze konieczny
Type: A Record
Host: @
Value: adres IP

```

Przechodzimy do katalogu

```
 cd /etc/nginx/sites-available/
```

Tworzymy i otwieramy plik w edytorze vim

```
vim mkzet
```

Wklejamy kod

```
server {
        server_name mkzet.pl www.mkzet.pl 46.41.143.70;
        listen 80;
        listen [::]:80;

        root /home/www/mkzet;

        # Add index.php to the list if you are using PHP
        index index.html index.htm index.nginx-debian.html;


        location / {
                try_files $uri /index.html;
        }

         location /api {
            proxy_pass http://localhost:3001;
            proxy_http_version 1.1;
            proxy_set_header Upgrade $http_upgrade;
            proxy_set_header Connection 'upgrade';
            proxy_set_header Host $host;
            proxy_cache_bypass $http_upgrade;
        }

}
```

Uaktywnienie naszej strony - linkuje pliki w katalogach

```
ln -s /etc/nginx/sites-available/mkzet /etc/nginx/sites-enabled/mkzet
```

Sprawdzamy ustawienia nginx-a czy nie ma błędu

```
nginx -t
```

Restart Nginx

```
systemctl reload nginx
```

<br>

Delete the default server configuration

```
 rm /etc/nginx/sites-available/default
 rm /etc/nginx/sites-enabled/default
```

Przechodzimy do katalogu /var/www/ i usówamy katalog html

```
rm -rf html
```

<br><br>

## 8. Certyfikat SSL with [Let's Encrypt](https://www.digitalocean.com/community/tutorials/how-to-secure-nginx-with-let-s-encrypt-on-ubuntu-20-04)

```
apt install certbot python3-certbot-nginx
```

Make sure that Nginx Full rule is available

```
ufw status
ufw allow 'Nginx Full'
ufw delete allow 'Nginx HTTP'
```

Przypisanie certyfikatów domenie i sub domenie ( ważność 90 dni ? )

```
certbot --nginx -d example.com -d www.example.com
certbot --nginx -d example.com -d www.example.com -d admin.example.com
```

timer that will run twice a day and automatically renew any certificate that’s within thirty days of expiration

```
systemctl status certbot.timer

```

To test the renewal process, you can do a dry run with certbot:

```
certbot renew --dry-run

```

---

<br><br>

Enable SSL with [Let's Encrypt](https://certbot.eff.org/lets-encrypt/ubuntubionic-nginx)
Instal snap

```
apt install snapd
```

Install Certbot

```
snap install --classic certbot

```

Prepare the Certbot command

```
ln -s /snap/bin/certbot /usr/bin/certbot

```

Get and install certificates using interactive prompt

```
certbot --nginx

```

<br><br>
<br><br>
<br><br>
<br><br>
<br><br>
<br><br>
<br><br>
<br><br>
<br><br>
<br><br>
<br><br>
<br><br>
<br><br>
<br><br>
<br><br>
<br><br>
apt install nano

## Instalacja Node.js

Pobranie repozytorium

```
curl -sL https://deb.nodesource.com/setup_8.x | sudo -E bash -
```

Instalacja

```
 sudo apt-get install -y nodejs
```

Instalacja build-essential

```
sudo apt-get install build-essential
```

Sprawdzamy wersję noda

```
node -v
```

---

## Instalacja Web serwera

Instalacja Nginx:

```
sudo apt-get update
sudo apt-get install nginx
```

<br>
<br>
<br>
<br>

## LINKS

- [Kurs Node.js + Express.js #12 - Deployment aplikacji (VPS)](https://www.youtube.com/watch?v=eaA8Ol6I16w)
- [Prosty i szybki deploy apki webowej Node.js na serwer VPS](https://www.youtube.com/watch?v=afwro39R6io)

https://www.youtube.com/watch?v=Nxw2j1-srVc&t=2427s

https://www.youtube.com/watch?v=Nxw2j1-srVc

https://www.youtube.com/watch?v=NjYsXuSBZ5U

---

---

---

<br>
<br>
<br>
<br>
# Node.js Deployment

> Steps to deploy a Node.js app to DigitalOcean using PM2, NGINX as a reverse proxy and an SSL from LetsEncrypt

## 1. Sign up for Digital Ocean

If you use the referal link below, you get $10 free (1 or 2 months)
https://m.do.co/c/5424d440c63a

## 2. Create a droplet and log in via ssh

I will be using the root user, but would suggest creating a new user

## 3. Install Node/NPM

```
curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -

sudo apt install nodejs

node --version
```

## 4. Clone your project from Github

There are a few ways to get your files on to the server, I would suggest using Git

```
git clone yourproject.git
```

### 5. Install dependencies and test app

```
cd yourproject
npm install
npm start (or whatever your start command)
# stop app
ctrl+C
```

## 6. Setup PM2 process manager to keep your app running

```
sudo npm i pm2 -g
pm2 start app (or whatever your file name)

# Other pm2 commands
pm2 show app
pm2 status
pm2 restart app
pm2 stop app
pm2 logs (Show log stream)
pm2 flush (Clear logs)

# To make sure app starts when reboot
pm2 startup ubuntu
```

### You should now be able to access your app using your IP and port. Now we want to setup a firewall blocking that port and setup NGINX as a reverse proxy so we can access it directly using port 80 (http)

## 7. Setup ufw firewall

```
sudo ufw enable
sudo ufw status
sudo ufw allow ssh (Port 22)
sudo ufw allow http (Port 80)
sudo ufw allow https (Port 443)
```

## 8. Install NGINX and configure

```
sudo apt install nginx

sudo nano /etc/nginx/sites-available/default
```

Add the following to the location part of the server block

```
    server_name yourdomain.com www.yourdomain.com;

    location / {
        proxy_pass http://localhost:5000; #whatever port your app runs on
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
```

```
# Check NGINX config
sudo nginx -t

# Restart NGINX
sudo service nginx restart
```

### You should now be able to visit your IP with no port (port 80) and see your app. Now let's add a domain

## 9. Add domain in Digital Ocean

In Digital Ocean, go to networking and add a domain

Add an A record for @ and for www to your droplet

## Register and/or setup domain from registrar

I prefer Namecheap for domains. Please use this affiliate link if you are going to use them
https://namecheap.pxf.io/c/1299552/386170/5618

Choose "Custom nameservers" and add these 3

- ns1.digitalocean.com
- ns2.digitalocean.com
- ns3.digitalocean.com

It may take a bit to propogate

10. Add SSL with LetsEncrypt

```
sudo add-apt-repository ppa:certbot/certbot
sudo apt-get update
sudo apt-get install python-certbot-nginx
sudo certbot --nginx -d yourdomain.com -d www.yourdomain.com

# Only valid for 90 days, test the renewal process with
certbot renew --dry-run
```

## Now visit https://yourdomain.com and you should see your Node app

---

---

<br>
<br>
<br>
<br>

# Backend Server Setup and Deployment

## Create Server

[Digital Ocean](https://m.do.co/c/ce761b3417ec) Welcome to the developer cloud. They make it simple to launch in the cloud and scale up as you grow—whether you’re running one virtual machine or ten thousand.

1. Create a \$5 Droptlet with Ubuntu 20.04, selecting a temporary password option.
2. Create a domain entry pointng to the server
3. Copy the IP Address when the server is created.
4. Login to the server with [Putty](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html) on Windows or ssh command on mac
   4.1 ssh root@SERVER_IP_ADDRESS

## Update Server

1. Update server components list with `apt update`
2. Upgrade server components with `apt upgrade`
3. Remove unused apps with `apt autoremove`
4. Restart `reboot now`

## Add Normal Sudo User and disable Root remote Login

1. `adduser username` Where username is the name that you want to use
   1.1 Type password and information needed
2. `usermod -aG sudo username` Where username is the user created in previous step
3. Test user conenction exits the server and acces now with `username` instead of `root`
4. Log back with root and execute `nano /etc/ssh/sshd_config`
5. Change `PermitRootLogin yes` to `PermitRootLogin no` and `#PermitEmptyPasswords no` to `PermitEmptyPasswords no`
6. Exit and save with `Ctrl+x` and then `Y` and finally `Enter`
7. Restart ssh with `/etc/init.d/ssh restart`
8. Exit the server

## Add Firewall

1. Login with your username account (not root)
2. Type `sudo ufw status` to view firewall status
3. Install Firewall with `sudo apt-get install ufw`
4. Enable Ports on Firewall
   4.1 `sudo ufw allow ssh`
   4.2 `sudo ufw allow http`
   4.3 `sudo ufw allow https`
5. Enable Firewall `sudo ufw enable`
6. Type `sudo ufw status` to view firewall status

## Install Nginx (HTTP Server)

1. Install with `sudo apt install nginx`
2. Start nginx `systemctl start nginx`

## Install Node

1. Install NVM with `curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.38.0/install.sh | bash`
2. Install Node.js with this command: `nvm install node`

## Install PM2

[PM2](https://pm2.keymetrics.io/) PM2 is a daemon process manager that will help you manage and keep your application online 24/7

1. `npm i -g pm2`

## Run API

1. Clone Github repo with `git clone GITHUB_REPO_URL`
2. Install project dependencies going inside the folder and type `npm install`
3. Create .env file with `nano .env`
4. Build the app with `npm run build`
5. Run in PM2 with `pm2 start npm --name "app name" -- start`
6. Save PM2 to run on server restart`pm2 startup`
7. Save current PM2 "state" with `pm2 save`

## Add Nginx Reverse Proxy information

1. `sudo nano /etc/nginx/conf.d/api.conf`
2. Type

```bash
server {
        listen          80;
        listen          [::]:80;
        server_name     api.rodolforoman.xyz;

        location / {
                proxy_pass http://localhost:3000;
        }

}
```

3. Exit and save with `Ctrl+x` and then `Y` and finally `Enter`
4. Test configuration with `sudo nginx -t`
5. Test configuration with `sudo nginx -s reload`

## Add Certbot to have Https on the server

```bash
    sudo snap install core; sudo snap refresh core
    sudo snap install --classic certbot
    sudo ln -s /snap/bin/certbot /usr/bin/certbot
    sudo certbot --nginx
```

---

---

<br>
<br>
<br>
<br>

# Connecting to the VPS

To connect your VPS server, you can use your server IP, you can create a root password and enter the server with your IP address and password credentials. But the more secure way is using an SSH key.

## Creating SSH Key

### For MAC OS / Linux / Windows 10 (with openssh)

1. Launch the Terminal app.
2. `ssh-keygen -t rsa`
3. Press `ENTER` to store the key in the default folder /Users/lamadev/.ssh/id_rsa).

4. Type a passphrase (characters will not appear in the terminal).

5. Confirm your passphrase to finish SSH Keygen. You should get an output that looks something like this:

```Your identification has been saved in /Users/lamadev/.ssh/id_rsa.
Your public key has been saved in /Users/lamadev/.ssh/id_rsa.pub.
The key fingerprint is:
ae:89:72:0b:85:da:5a:f4:7c:1f:c2:43:fd:c6:44:30 lamadev@mac.local
The key's randomart image is:
+--[ RSA 2048]----+
|                 |
|         .       |
|        E .      |
|   .   . o       |
|  o . . S .      |
| + + o . +       |
|. + o = o +      |
| o...o * o       |
|.  oo.o .        |
+-----------------+
```

6. Copy your public SSH Key to your clipboard using the following code:
   `pbcopy < ~/.ssh/id_rsa.pub`

### For Windows

1. Download PuTTY and PuTTYgen.
2. Open up PuTTYgen and click the `Generate`.
3. Copy your key.
4. Enter a key passphrase and confirm.
5. Save the private key.

## Connection

After copying the SSH Key go the to hosting service provider dashboard and paste your key and save. After,

### For MAC OS / Linux

```bash
ssh root@<server ip address>
```

### For Windows

1. Open the PuTTY app.
2. Enter your IP address.
3. Open the following section:
   Connection - SSH - Auth
4. Browse the folders and choose your private key.

## First Configuration

### Deleting apache server

```
systemctl stop apache2
```

```
systemctl disable apache2
```

```
apt remove apache2
```

to delete related dependencies:

```
apt autoremove
```

### Cleaning and updating server

```
apt clean all && sudo apt update && sudo apt dist-upgrade
```

```
rm -rf /var/www/html
```

### Installing Nginx

```
apt install nginx
```

### Installing and configure Firewall

```
apt install ufw
```

```
ufw enable
```

```
ufw allow "Nginx Full"
```

## First Page

#### Delete the default server configuration

```
 rm /etc/nginx/sites-available/default
```

```
 rm /etc/nginx/sites-enabled/default
```

#### First configuration

```
 nano /etc/nginx/sites-available/netflix
```

```
server {
  listen 80;

  location / {
        root /var/www/netflix;
        index  index.html index.htm;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
        try_files $uri $uri/ /index.html;
  }
}

```

```
ln -s /etc/nginx/sites-available/netflix /etc/nginx/sites-enabled/netflix

```

##### Write your fist message

```
nano /var/www/netflix/index.html

```

##### Start Nginx and check the page

```
systemctl start nginx
```

## Uploading Apps Using Git

```
apt install git
```

```
mkdir netflix
```

```
cd netflix
```

```
git clone <your repository>
```

## Nginx Configuration for new apps

```
nano /etc/nginx/sites-available/netflix
```

```
location /api {
        proxy_pass http://45.90.108.107:8800;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
  }
```

##### If you check the location /api you are going to get "502" error which is good. Our configuration works. The only thing we need to is running our app

```
apt install nodejs
```

```
apt install npm
```

```
cd api
```

```
npm install
```

```
nano .env
```

##### Copy and paste your env file

```
node index.js
```

#### But if you close your ssh session here. It's gonna kill this process. To prevent this we are going to need a package which is called `pm2`

```
npm i -g pm2
```

Let's create a new pm2 instance

```
pm2 start --name api index.js
```

```
pm2 startup ubuntu
```

## React App Deployment

```
cd ../client
```

```
nano .env
```

Paste your env file.

```
npm i
```

Let's create the build file

```
npm run build
```

Right now, we should move this build file into the main web file

```
rm -rf /var/www/netflix/*
```

```
mkdir /var/www/netflix/client
```

```
cp -r build/* /var/www/netflix/client
```

Let's make some server configuration

```
 location / {
        root /var/www/netflix/client/;
        index  index.html index.htm;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
        try_files $uri $uri/ /index.html;
  }

```

### Adding Domain

1 - Make sure that you created your A records on your domain provider website.

2 - Change your pathname from Router

3 - Change your env files and add the new API address

4 - Add the following server config

```
server {
 listen 80;
 server_name safakkocaoglu.com www.safakkocaoglu.com;

location / {
 root /var/www/netflix/client;
 index  index.html index.htm;
 proxy_http_version 1.1;
 proxy_set_header Upgrade $http_upgrade;
 proxy_set_header Connection 'upgrade';
 proxy_set_header Host $host;
 proxy_cache_bypass $http_upgrade;
 try_files $uri $uri/ /index.html;
}
}

server {
  listen 80;
  server_name api.safakkocaoglu.com;
  location / {
    proxy_pass http://45.90.108.107:8800;
    proxy_http_version 1.1;
    proxy_set_header Upgrade $http_upgrade;
    proxy_set_header Connection 'upgrade';
    proxy_set_header Host $host;
    proxy_cache_bypass $http_upgrade;
    }
}

server {
  listen 80;
  server_name admin.safakkocaoglu.com;
  location / {
    root /var/www/netflix/admin;
    index  index.html index.htm;
    proxy_http_version 1.1;
    proxy_set_header Upgrade $http_upgrade;
    proxy_set_header Connection 'upgrade';
    proxy_set_header Host $host;
    proxy_cache_bypass $http_upgrade;
    try_files $uri $uri/ /index.html;
  }
}
```

## SSL Certification

```
apt install certbot python3-certbot-nginx
```

Make sure that Nginx Full rule is available

```
ufw status
```

```
certbot --nginx -d example.com -d www.example.com
```

Let’s Encrypt’s certificates are only valid for ninety days. To set a timer to validate automatically:

```
systemctl status certbot.timer
```
