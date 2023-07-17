## Create Your AWS Instance

- You can create whatever AWS instance you want. 
- Here are the recommendations:
	- Image: latest Ubuntu
	- Instance Type: t2.micro
	- **Download the key pair file based on your OS.**
	- Network Settings: 4 security rules

| **Type**   | **Port Range** | **Source Type** | **Source** |
|------------|----------------|-----------------|------------|
| ssh        | 22             | Anywhere        | 0.0.0.0/0  |
| HTTP       | 80             | Anywhere        | 0.0.0.0/0  |
| Custom TCP | 1024-1048      | Anywhere        | 0.0.0.0/0  |
| Custom TCP | 20-21          | Anywhere        | 0.0.0.0/0  |

## Connect to Your Instance From Your Local Machine

### Linux and macOS
1. Open Terminal.
2. Navigate to the directory that contains your key pair file (.pem).
3. Enter the following command to allow your key pair file.
```
chmod 600 <key pair name>.pem
```
4. Connect to your instance with the following command:
```
ssh -i "<key pair name>.pem" ubuntu@<AWS instance public dns>
```
5. If you get "Are you sure you want to continue connecting?", type **yes** and press **Enter**.
6. You should be connected now!
7. To close your connection, type **exit**.

### Windows
1. Install [PuTTY](https://www.chiark.greenend.org.uk/~sgtatham/putty/) and open in.
2. In the **Category** pane, choose **Session**.
	1. In the **Host Name** body, enter ubuntu@<AWS instance public dns>.
	2. Make sure the **Port** value is **22**.
	3. Under **Connection type**, select **SSH**.
3. In the **Category** pane, expand **Connection**, expand **SSH**, expand **Auth**, and the select **Credentials**.
	1. Click **Browse**.
	2. Select your key pair file (.ppk).
4. If you get "The host key is not cached for this server.", select **Accept**.
5. You should be connected now!
6. To close your connection, close PuTTY.

## Install Web Server Software

### LAMP

*Linux, Apache, MySQL, and PHP*

- The web document root for your web server is **var/www/html**.
- Enter the following commands one at a time while connected to your AWS Instance.

```
sudo apt-get update
```

```
sudo apt-get install apache2
```
- When it asks to continue, allow it to.

```
sudo apt-get install mysql-server
```
- When it asks to continue, allow it to.

```
sudo apt-get install php
```
- When it asks to continue, allow it to.

```
sudo apt-get install libapache2-mod-php-y
```

```
sudo /etc/ini.d/apache2 restart
```

```
sudo mysql -u root -p
```
- Press Enter when it asks for a password.
- You should get a `mysql>` prompt.
- Enter the following to change your password.
- *Note: this doesn't work and I don't know why yet*
```
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY '<password>';
```
- Exit the `mysql>` prompt with `Exit`.

```
sudo service mysql stop
```

```

### phpMyAdmin for MySQL
