# ZTE MF258 router SSH access

Guide on how to access SSH on the ZTE router

Attention! You do so at your own risk

## Step 1
Login to WebInterface (192.168.1.1) and download `Backup Configuration File`

<img src="https://github.com/realiis/zte-mf258-ssh-access/raw/master/backuprestore.png">

## Step 2
Change name file:
```
mv config.cfg config.gz
```

Extract file:
```
gzip -d config.gz
```

Extract the file again
```
tar -xf config
``` 

## Step 3
Open `etc/shadow` and copy hash root (example on screenshot):

<img src="https://github.com/realiis/zte-mf258-ssh-access/raw/master/etcshadow.png">
  
and paste the copied hash into the page https://www.tunnelsup.com/hash-analyzer/ and copy the `salt`:

<img src="https://github.com/realiis/zte-mf258-ssh-access/raw/master/salt.png">

## Step 4

Create a new hash:
```
openssl passwd -1 -salt <salt from Step 3> <new password>
```

Example:

<img src="https://github.com/realiis/zte-mf258-ssh-access/raw/master/openssl.png">

## Step 5
Paste new hash in place of old hash in the `etc/shadow`:

<img src="./etcshadow.png">

## Step 6
Create a new archive:
```
rm config
tar -cf config etc/ www/
gzip config
mv config.gz config.cfg
```

## Step 7
Upload a new configuration file on the WebInterface:

<img src="asd">

## Step 8

Connect to router SSH with your new password:

```
ssh root@192.168.1.1
```
