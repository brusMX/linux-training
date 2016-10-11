# Using Azure CLI to provision the VM
1. We will be using Azure CLI, if you don't have it you can find it [here](https://azure.microsoft.com/en-us/documentation/articles/xplat-cli-install/)
1. We login into our account
    ```Shell
    azure login
    ...
    info:    Executing command login
    \info:    To sign in, use a web browser to open the page https://aka.ms/devicelogin. Enter the code XXXXXXXX to authenticate.
    info:    Added subscription Linux Apps - brmedi
    info:    login command OK
    ```
1. We need to make sure our subsc is on ARM mode type the following:
    ```Shell
    azure 
    ```
    Notice that at the end of you will see the mode:
    ```Shell
    help:    Current Mode: arm (Azure Resource Management)
    ```
    If you are not using ARM you need to enter the following command:
    ```Shell
    azure config mode arm
    ...
    info:    Executing command config mode
    info:    New mode is arm
    info:    config mode command OK
    ```

1. We create a resource group for this excercise. The syntax is the following:
     ```Shell
    resource create [options] <resource-group> <name> <resource-type> <location> <api-version>
    ```
    For me it would be something like this:
    ```Shell
    azure resource create rhel-demo -l westus
    ```
1. Now lets deploy the vm using the JSON file of the template
     ```Shell
    azure group deployment create <resource-group> <my-deployment-name> --template-uri azuredeploy.json
    ```


1. Make sure to copy the full public key from the terminal and paste it to you VM's definition.
    ![alt text][set-vm-up]


[set-vm-up]: /img/set-vm-up.jpg "Fill it up with your info."
