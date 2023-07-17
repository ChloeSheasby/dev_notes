## Create Your AWS Instance

- You can create whatever AWS instance you want. 
- Here are the recommendations:
	- Image: latest Ubuntu
	- Instance Type: t2.micro
	- Network Settings: 4 security rules

| **Type**   | **Port Range** | **Source Type** | **Source** |
|------------|----------------|-----------------|------------|
| ssh        | 22             | Anywhere        | 0.0.0.0/0  |
| HTTP       | 80             | Anywhere        | 0.0.0.0/0  |
| Custom TCP | 1024-1048      | Anywhere        | 0.0.0.0/0  |
| Custom TCP | 20-21          | Anywhere        | 0.0.0.0/0  |

## Connect to Your Instance From Your Local Machine

## Install Web Server Software

### LAMP
### phpMyAdmin for MySQL
