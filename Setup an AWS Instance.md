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
### Windows

## Install Web Server Software

### LAMP
### phpMyAdmin for MySQL
