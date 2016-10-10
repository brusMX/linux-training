# Connect to your VM using Bash (For Mac, Linux and Windows 10 with Bash installed)

1. Make sure to copy the full public key from the terminal and paste it to you VM's definition.
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
  And you should see your server, something like this:

            Welcome to Ubuntu 15.10 (GNU/Linux 4.2.0-23-generic x86_64)
            * Documentation:  https://help.ubuntu.com/

            Get cloud support with Ubuntu Advantage Cloud Guest:
                http://www.ubuntu.com/business/services/cloud

            84 packages can be updated.
            61 updates are security updates.

            Last login: Mon Apr  4 01:04:56 2016 from 189.147.6.184
            brus@brusulubuntu:~$ 


[set-vm-up]: ../img/set-vm-up.jpg "Fill it up with your info."
