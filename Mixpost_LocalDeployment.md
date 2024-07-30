># Mixpost setup in Local machine

---

## If you are using windows then use `WSL` command to run the following commands  

#### Open the Command prompt Get into Directory where you need to insall a mixpost in you local machine and run

```
WSL --install 
```

Restart the system

After restarting open the `CMD` and get into the directory like C drive or D drive  

```
WSL
```

It will ask password for to login as a root user in Ubuntu machine

Once done with Ubuntu installation run the following commands

># **Requirements**
>
- ## **Software**

1. Installing `PHP >= 8.2.0 `, `maria-db` ,` Web Server `, `composer`
   ```
   sudo apt update 
   sudo apt install php libapache2-mod-php apache2 composer mariadb-server -y
   ```
2. Installing `Supervisor` , `FFmpeg `, `Redis 6.2 or higher`
   
   ```
   sudo apt install redis-server supervisor ffmpeg -y
   ```
3. Installing  `Curl` , `Zip `,  `Unzip`

   ```
   sudo apt install zip unzip curl -y
   ```

- ## **PHP Extension**

   Installing php extenstion like `curl`, `mysql`,   `bcmath`,`gd` ,`mbstring`, `redis`, `xml`,`zip`, `intl`
  -  Check the version of php `php -v` and install the extension accordingly
  
 If verion is `8.2` then follow below step 
 ```
 sudo apt install php8.2-curl php8.2-mysql php8.2-bcmath php8.2-gd php8.2-mbstring php8.2-redis php8.2-xml php8.2-zip php8.2-intl
 ```
 If verion is `8.3` then follow below step 

  ```
    sudo apt install php8.3-curl php8.3-mysql php8.3-bcmath php8.3-gd php8.3-mbstring php8.3-redis php8.3-xml php8.3-zip php8.3-intl -y
  ```


> # Steps to install mixpost

## Step 1 : **Clone the repository from github**

Open CMD and get into the directory In C drive or D drive run the following commands

Install a composer 

   ```
   cd DigiMe
   composer install
   ```
## Step 2 : **Setting up .env file**
Get into a maria-db and set a  `password`

  ```
  mysql 

  ALTER USER 'root'@'localhost' IDENTIFIED BY '<Password>';

  exit
  ```
Copy the `.env.example` file and create `.env` file Adjust the  file settings to match your project requirements like `DB_DATABASE`, `DB_USERNAME` , `DB_PASSWORD` , `APP_DEBUG`, `APP_URL` change into `<http://localhost>`

In `Password`  you can modify the with your own value
  ```
  cp .env.example .env
  sudo nano .env 
  ```

## Step 3 : **Installing Dependency**

  ```
  sudo php artisan mixpost:setup-gitignore
  sudo php artisan queue:batches-table
  sudo php artisan mixpost:publish
  sudo php artisan storage:link
  ```
## Step 4 : **File Permissions**

Get into the mixpostapp directory and Change the file permission

  ```
  cd mixpostapp
  chmod -R 755 public
  chmod -R 775 storage
  chmod -R 775 bootstrap/cache
  ```

## Step 5:  **Application Configuration**

**Optimize application**

  ```
  php artisan optimize
  ```

**Migrate tables**

  ```
  php artisan migrate
  ```

## Step 6 : **Create the first user**

You can create an initial user by executing

  ```
  php artisan mixpost-auth:create
  ```

## Step 7: **Setting Up Process Supervision**
Create `mixpost_horizon.conf` file inside of `/etc/supervisor/conf.d` folder and put this content
  ```
  [program:mixpost_horizon]
  process_name=%(program_name)s
  command=php /<path to your project>/artisan serve --host=0.0.0.0 --port=8080
  directory=/path to your project/
  autostart=true
  autorestart=true
  stopwaitsecs=3600
  ```
Once the configuration file has been created,Get into a project directory and  you may update the Supervisor configuration and start the processes using the following commands:
  ```
  sudo supervisorctl reread
 
  sudo supervisorctl update
 
  sudo supervisorctl start mixpost_horizon:*
  ```
## Step 8 : **Access Mixpost**

Navigate to `http://localhost:8080`  and the mixpost should appear with the login screen you can login throught a credentials which you provided in step 6 
