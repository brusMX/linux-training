# Set up your Virtual Machine


## Create a pair of SSH keys using Bash (For Mac, Linux and Windows 10 with Bash installed)
1. Use *'ssh-keygen'* to create an RSA SSH key of 4096 bits pointing to our e-mail address.
    
    ```Shell
    ssh-keygen -t rsa -b 4096 -C "mymail@brus.ml"
    ```

1. After this command you will be asked for a location to save your powerful key, you can give it a custom location but it's not really necessary unless you actually handle multiple keys.

    ```Shell      
    Enter a file in which to save the key (/Users/you/.ssh/id_rsa): [Press enter]
    ```

2. Now you will be asked to enter a password to increase the level of security of your key. This password is optional, but if you decide to set it up you will need to enter it every time you interact with your SSH private key:

    ```Shell
        Enter passphrase (empty for no passphrase): [Type a passphrase]
        Enter same passphrase again: [Type passphrase again]
    ``` 

3. Now, after your key has been created just *cat* the content of your public key (if you used a different location, make sure you use the correct file). This is the 

```Shell
    code ~/.ssh/id_rsa.pub
    [This is an example of how and your pub key should look like:]
    ssh-rsa 123456789/dTc6wJT+YCOUiLLS6F7Ge4WlCgmH7fW7UIUJpFcXwDv1bWVMQ3chBFFELWEhEjCqX7HAVoSjEF8oAwM0Ik5p6y66J420eeOGBLHkyV+nBiV0F5WVRKFS5Az1rZy8x/1usbMms/skMnS5Int9QcGIIA9g7Ws9xg28/2XA5IUPUZ0kIKbuSv7bAIqrHaH7WXzUeLeOjUIeW34d9WO52kNqiITjyW1D7kThXKtgS9Y5TEie5MuP8plzz+mBID59EFmdEhBK7QquuT6axI1PIDNm4PrhI7mJP9IgRRQOOXZ1rvoysOHxhDvzVWRuc623pV8PPjiBHiu1Y1T mymail@brus.ml
```
## Connect to your VM using Bash (For Mac, Linux and Windows 10 with Bash installed)

1. Make sure to copyu the full public key from the terminal and paste it to you VM's definition.
    ![alt text][set-vm-up]

2. SSH into your VM. Make sure you replace "myUserName" with your VM's user name and the url should be your "DNS name" or the IP from the VM's details.

    
```Shell
ssh myUserName@myDomainName.cloudapp.net
```

Since its a new connection you will have to confirm adding the key to the list of known hosts.

```Shell
The authenticity of host 'myDomainName.cloudapp.net (14.81.161.17)' can't be established.
ECDSA key fingerprint is SHA256:Fy9G/qkO9msNo6JpcBT3SL4Qz1BMWB9iasTAJ6VrvjbPS.
Are you sure you want to continue connecting (yes/no)? yes [Type 'yes' and enter]
Warning: Permanently added 'myDomainName.cloudapp.net,14.81.161.17' (ECDSA) to the list of known hosts.
```

And because we are securing our SSH session with SSH-RSA (type of key), we will not be prompted for the VM's password. But you will be asked for the private key's passphrase if you defined one when you created it. 
    
    
            Welcome to Ubuntu 15.10 (GNU/Linux 4.2.0-23-generic x86_64)
            Documentation:  https://help.ubuntu.com/

            Get cloud support with Ubuntu Advantage Cloud Guest:
                http://www.ubuntu.com/business/services/cloud

            83 packages can be updated.
            61 updates are security updates.

            The programs included with the Ubuntu system are free software;
            the exact distribution terms for each program are described in the
            individual files in /usr/share/doc/*/copyright.

            Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
            applicable law.

            To run a command as administrator (user "root"), use "sudo <command>".
            See "man sudo_root" for details.

            _____________________________________________________________________
            WARNING! Your environment specifies an invalid locale.
            This can affect your user experience significantly, including the
            ability to manage packages. You may install the locales by running:

            sudo apt-get install language-pack-UTF-8
                or
            sudo locale-gen UTF-8

            To see all available language packs, run:
            apt-cache search "^language-pack-[a-z][a-z]$"
            To disable this message for all users, run:
            sudo touch /var/lib/cloud/instance/locale-check.skip
            _____________________________________________________________________

            myUserName@myDomainName:~$ 

**SO, WE ARE IN!**
    
*Note: If the server is asking you for a password, but you set up a passwordless connection, it could mean that SSH is not finding your pair of keys on this terminal session. Use `ssh -v` option to make it easier to find the problem with a verbose connection.
Sometime you need to make sure that your key is valid and is set to your terminal with `ssh-add` read [this](http://stackoverflow.com/questions/17846529/could-not-open-a-connection-to-your-authentication-agent).
You can also specify that you are using the correct SSH key with `ssh -i path/to/key`.
In the worst case scenario, remember you can reset your SSH key and user name in the portal.*

## Customize your connection using the `~/.ssh/config` file (For Mac, Linux and Windows 10 with Bash installed)

Your life can be easier if you can create a `config` file on `.ssh` folder.

```Shell
    touch ~/.ssh/config
    code ~/.ssh/config
```   
You can take the following lines as an example, just make sure to replace the relevant information and save it after you are done:

```Shell
    Host myVM
        HostName myDomainName.cloudapp.net
        User myUserName
        Port 22
        IdentityFile ~/.ssh/id_rsa
```

*NOTE: Make sure that the identity file is the private key (not the `.pub` file) that you created in the **"Create an SSH key"** step, it should be right next to the `.pub` file but without an extension or with the `.key` extension.

With this change done you can easily start your SSH connection by only using the Host you defined in the config file, you don't longer need to remember the user name nor the parameters or each VM.

```Shell
    ssh myVM
```
    
    
## Create a pair of SSH Keys using PuTTY (Windows)

1. After you have installed PuTTY, you will need to open PuTTYgen.  Make sure you use *'SSH-2 RSA'* and *'4096'* bits and click on *'Generate'*
![alt text][puttygen]

1. Start moving your cursor in the indicated blank area until you fill up the green bar.
![alt text][puttygen-mouse]

1. The program will take a moment to generate your keys
![alt text][puttygen-generate]

1. As a result you will obtain your public key, you can go ahead and copy that in your server's configuration.
![alt text][puttygen-done]

1. Now lets save (both) your public and private key. You can manage your private key in a safer manner by using a Key passphrase (this passphrase will be required every time you interact with your private key).
![alt text][puttygen-keys]

1. The next thing we need to do is open PuTTY and use our brand new generated key to connect to our server.
![alt text][putty]

1. On the left menu go to *'Connection'* > *'SSH'* > *'Auth'*. And click on *'Browse'* to select the *'.ppk'* file you just created.
![alt text][putty-select]

1. Go back to the *'Session'* Category in the menu, put down the URL/IP of your server, write down a custom name for your connection and click on *'Save'*. Now every time you want to connect to that server you can load that configuration
![alt text][putty-save]



1. Select the "pricing tier" that suits your needs. Please remember that you can select more pricing tiers from the "View All" option.
    ![alt text][pricing]
1. Confirm the "Network" settings on your VM. You don't really need to change anything here unless you want to customize something like your "Domain Name".
    ![alt text][network]
1. Select or create a new Storage Account. If you already have an Storage Account that can be used for your VM, you just need to select it from here.
    ![alt text][storage]
1. Add rules to your VM. In order for us to see the web pages served by our VM we will have to allow HTTP and HTTPS traffic, that means that we need to create an allow rule for port 80 and another one for 443.
    ![alt text][rules]
1. Finally, we select the location of our VM and "Create" our VM. For this purpose, any data center would do. Now, my advice would be to use a region that is close to your business, also if you need it here is a [list](https://azure.microsoft.com/en-us/regions/#services) of services available by region.
After you click on create you can see the progress of the deployment on you notifications.
    ![alt text][status]
    ![alt text][done]
1. **Let's take it for a ride!** So finally we have our brand new toy deployed, lets verify if it's up and running.
    1. Go to your new VM's details. As you can see in the image the app is up and running, it has a DNS name and an IP.
        ![alt text][vm-details]
 

    And you should see your server, something like this:

            Welcome to Ubuntu 15.10 (GNU/Linux 4.2.0-23-generic x86_64)
            * Documentation:  https://help.ubuntu.com/

            Get cloud support with Ubuntu Advantage Cloud Guest:
                http://www.ubuntu.com/business/services/cloud

            84 packages can be updated.
            61 updates are security updates.

            Last login: Mon Apr  4 01:04:56 2016 from 189.147.6.184
            brus@brusulubuntu:~$ 

    1. **Let's try docker.** Let's remember this VM has docker pre-installed. So run the following command:
    ```Shell
    docker run hello-world
    ```
    So after a few seconds we should have an output like this:

            Unable to find image 'hello-world:latest' locally
            latest: Pulling from library/hello-world
            03f4658f8b78: Pull complete 
            a3ed95caeb02: Pull complete 
            Digest: sha256:8be990ef2aeb16dbcb9271ddfe2610fa6658d13f6dfb8bc72074cc1ca36966a7
            Status: Downloaded newer image for hello-world:latest

            Hello from Docker.
            This message shows that your installation appears to be working correctly.

            To generate this message, Docker took the following steps:
            1. The Docker client contacted the Docker daemon.
            2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
            3. The Docker daemon created a new container from that image which runs the
                executable that produces the output you are currently reading.
            4. The Docker daemon streamed that output to the Docker client, which sent it
                to your terminal.

            To try something more ambitious, you can run an Ubuntu container with:
            $ docker run -it ubuntu bash

            Share images, automate workflows, and more with a free Docker Hub account:
            https://hub.docker.com

            For more examples and ideas, visit:
            https://docs.docker.com/userguide/
            
            
   The cool thing behind docker is that if we run this command again, we won't have to download the image again. It will re-use the image that we just downloaded :)
   
[vscode]: ../img/vscode.jpg "Visual Studio Code works like a charm"
[docker-in-marketplace]: ../img/docker-in-marketplace.jpg "Azure Marketplace."
[docker-in-azure]: ../img/docker-vm-in-azure.jpg "Docker VM in Azure ready to be deployed."
[set-vm-up]: ../img/set-vm-up.jpg "Fill it up with your info."
[pricing]: ../img/pricing-tiers.jpg "Click 'View more' to see more options."
[network]: ../img/network-conf.jpg "You can use this section to customize your VM's network."
[storage]: ../img/storage-conf.jpg "You can create a new storage account or use one previously created."
[rules]: ../img/rules-conf.jpg "Allow access to the VM with Endpoint Rules."
[status]: ../img/deployment-status.jpg "Your VM is being deployed."
[done]: ../img/deployment-done.jpg "Your VM was successfully deployed."
[vm-details]: ../img/vm-details.jpg "Your VM's details"
[reset]: ../img/reset-password.jpg "Don't worry if you forgot your credentials, you can always reset them"
[puttygen]: ../img/puttygen.jpg "PuTTYgen is the tool that allows you to create your SSH access keys"
[puttygen-mouse]: ../img/puttygen-mouse.jpg "Move your mouse to generate the key"
[puttygen-generate]: ../img/puttygen-gen.jpg "The time it takes depends on how strong you chose the key to be"
[puttygen-done]: ../img/puttygen-done.jpg "You can also add comments to the key"
[puttygen-keys]: ../img/puttygen-keys.jpg "You can use txt as an extension for your public key if you prefer it"
[putty]: ../img/putty.jpg "You can use txt as an extension for your public key if you prefer it"
[putty-select]: ../img/putty-select.jpg " "
[putty-save]: ../img/putty-save.jpg "You can save your changes every time you want"