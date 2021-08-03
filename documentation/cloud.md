# Virtual machines

General practices are:

## VM tagging

Testnode
:   meant to do only tests

Worknode
:   meant for work

# Azure

## Setting up

[How to quickly connect to a Linux VM with SSH \| Azure Tips and Tricks -
YouTube](https://www.youtube.com/watch?v=7pmn6luCwQ4)

1.  During the creation of the VM you have to download a PEM file and
    store in `~/.ssh/` folder.
    -   After the VM is created, to the general view and click on
        \"Connect\" then SSH. On step 3 type the path to this PEM file.
    -   Copy the command on step 4 and paste on the terminal.
2.  Desktop configuration:
    -   inside the vm, update the mirrors by using `apt update` and the
        upgrade by running `apt dist-upgrade`

    ```bash

    sudo apt update sudo apt dist-upgrade
    ```

    -   install the packages that are needed for the desktop environment
        (since Azure has a better connection, the Gnome desktop could run
        satisfactorily)

    ```bash
    sudo apt install ubuntu-gnome-desktop
    ```
3.  Configure VNC:

    ```bash
    apt install tightvncserver
    ```

4.  Reboot the machine
5.  Install a VNC Client - Remmina (on the local machine)

    ```bash
    sudo apt install remmina
    ```

6.  Create a startup script:
    -   SSH into the linode
    -   Test if the VNC server is running normally by entering

    ```bash
    vncserver :1
    ```
    Type in the password and type "n" for the question. It
    should appear "New 'X' desktop is localhost:1".

    -   After this, we have to change the file that was just created inside
        the VM because there are more things to set up first.

    ```bash
    vncserver -kill :1 cd ~/.vnc && ls -l # look for xstartup file and
    change that file mv xstartup xstartup-old # changed 
    vim xstartup # create a new version of that file
    ```

    -   Inside the `xstartup` file type the following bash script, this
        creates a MATE session when the VNC server is run on startup

    ```
    \#!/bin/bash

    exec /usr/bin/mate-session &
    ```

    -   Make this new script executable

    ```bash
    chmod +x xstartup
    ```

    -   Disconnect from the linode

    ```bash
    logout
    ```

7.  Alternatively, use x11vnc.service [How to install x11vnc vnc server
    as a service on Ubuntu 20.04, for remote
    acc...](https://www.crazy-logic.co.uk/projects/computing/how-to-install-x11vnc-vnc-server-as-a-service-on-ubuntu-20-04-for-remote-access-or-screen-sharing)
    [Ubuntu VNC Server -
    YouTube](https://www.youtube.com/watch?v=3K1hUwxxYek)
8.  Set up a secure connection: set a ssh tunnel

    ```bash
    ssh -i \~/.ssh/ubuntu.pem -L 5901:ip-address:5901 lucas\@ip-address
    ```
9.  Connect to the server:
    -   Inside the VM start the VNC server.
    -   Open Remmina
    -   Create a new profile \"+\"
    -   Choose name
    -   Choose group
    -   Choose protocol: VNC plugin
    -   Basic - Server: \"localhost:1\"
    -   Set color depth and quality for best experience
    -   Save
2.  Using the remote desktop: choose the profile and start using

## How to cut costs

[Top 10 Tricks To Save Money With Azure Virtual Machines \|
Build5Nines](https://build5nines.com/top-10-tricks-to-save-money-with-azure-virtual-machines/)

## Useful links

-   [Introdução às máquinas virtuais do Azure - Learn \| Microsoft
    Docs](https://docs.microsoft.com/pt-br/learn/modules/intro-to-azure-virtual-machines/)
-   [Containers vs VMs: What\'s the difference? -
    YouTube](https://www.youtube.com/watch?v=cjXI-yxqGTI)
    -   VMs (bottom \> top)
        -   Hardware \> Hypervisor - responsible for creating
            virtualized instances of components for VMs
        -   Achieves machine isolation
        -   A common use would be to have a Server at lower level that
            uses the hypervisor to create a number of independent
            machines for each other
        -   Hypervisor example is VirtualBox, Boxes or Hyper-V
    -   Containers
        -   Hardware \> Kernel \> Host OS \> Each container running (C1,
            C2, ...)
        -   Containers share hardware resources but each application
            runs independently from each other
-   [🌌 How to use Microsoft Hyper-V on Windows 10 to create virtual
    machines - You...](https://www.youtube.com/watch?v=3I64TeJ4iNI)
-   [Deploy Xfce
    Desktop](https://azure.microsoft.com/pt-br/resources/templates/ubuntu-desktop-xfce-rdp/)

## How to recover access to SSH

[Como recuperar acesso ssh ao Linux no Azure Portal ou Azure CLI -
YouTube](https://www.youtube.com/watch?v=NzLxk39iTww)

## Managing multiple VMs

## Azure CLI

-   [Azure CLI Tutorial -
    YouTube](https://www.youtube.com/watch?v=GqpwiyYsNIw&pp=ugMICgJwdBABGAE%3D)
-   [Install the Azure CLI for Linux manually \| Microsoft
    Docs](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli-linux?pivots=apt)
-   [Introdução à CLI do Azure \| Microsoft
    Docs](https://docs.microsoft.com/pt-br/cli/azure/get-started-with-azure-cli)

## Deploying VMs

1.  Ubuntu w/ Xfce

    ``` {.bash}
    az group deployment create \
        --resource-group <my-resource-group> --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/demos/ubuntu-desktop-xfce-rdp/azuredeploy.json

    ```

2.  Ubuntu w/ Gnome

    [Ubuntu Gnome Desktop, VS Code, Azure CLI and RDP
    Support](https://azure.microsoft.com/pt-br/resources/templates/ubuntu-desktop-gnome-rdp/)

# Linode

This are the steps to create a Ubuntu 20.04 LTS VM inside Linode. Master
ref: [Linux Desktop in the Cloud Tutorial \| Create and Access From
Anywhere - YouTube](https://www.youtube.com/watch?v=633OWaW3cyo) This is
essentially a transcriptions of the steps.

1.  Create a Linode:
    -   choose the right image,
    -   the region that has the lowest ping,
    -   type of plan,
    -   label,
    -   tags (testnode or worknode),
    -   choose strong password,
    -   click ****Create****.
2.  Configure your desktop:
    -   check if the VM is already up clicking \"Launch LISH Console\",
    -   ssh into the vm

    ```bash
    ssh root\@ip.adress
    ```

    -   inside the vm, update the mirrors by using `apt update` and the
        upgrade by running `apt dist-upgrade`

    ```bash
    apt update apt dist-upgrade
    ```

-   install the packages that are needed for the desktop environment
    (since it is ubuntu, you have to choose one of the versions already
    supported and because this is a mere transcription from what was
    done in the video it will be installed MATE desktop); this step can
    take a while to complete.

    ```bash
    apt install ubuntu-mate-desktop
    ```

3.  Configure VNC:

    ```bash
    apt install tightvncserver
    ```

4.  Create a user:

    ```bash
    adduser lucas ls -l *home* # test if the user was created usermod -aG
    sudo lucas # include lucar in the group sudo su - lucas \# switch to
    the user lucas sudo apt update # test if it working
    ```
    At the end, reboot the machine.

5.  Install a VNC Client - Remmina (on the local machine)

    ```bash
    sudo apt install remmina
    ```

6.  Create a startup script:
    -   SSH into the linode
    -   Test if the VNC server is running normally by entering

    ```bash
    vncserver :1
    ```
    Type in the password and type "n" for the question. It
    should appear "New 'X' desktop is localhost:1".

    -   After this, we have to change the file that was just created inside
        the VM because there are more things to set up first.

    ```bash
    vncserver -kill :1 
    cd ~/.vnc && ls -l # look for xstartup file and change that file 
    mv xstartup xstartup-old # changed 
    vim xstartup # create a new version of that file
    ```

    -   Inside the `xstartup` file type the following bash script, this
        creates a MATE session when the VNC server is run on startup

    ```bash
    #!/bin/bash

    exec /usr/bin/mate-session &
    ```

    -   Make this new script executable

    ```bash
    chmod +x xstartup
    ```

    -   Disconnect from the linode

    ```bash
    logout
    ```

7.  Set up a secure connection: set a ssh tunnel

    ```bash
    ssh -L 5901:ip-address:5901 lucas@ip-address
    ```

8.  Connect to the server:
    -   Inside the VM start the VNC server.
    -   Open Remmina
    -   Create a new profile "+"
    -   Choose name
    -   Choose group
    -   Choose protocol: VNC plugin
    -   Basic - Server: "localhost:1"
    -   Set color depth and quality for best experience
    -   Save
9.  Using the remote desktop: choose the profile and start using

## General impressions

Not great, Azure is a lot better because the server are closer, simple
as that.

# Google Cloud

## How to set up a VM

[Set up VM on Google Cloud Platform (GCP) + SSH setup -
YouTube](https://www.youtube.com/watch?v=2NTcO7BjOJE) One the
interesting features on Google Cloud is that you can create instances of
VMs first and than create a proper VM from that template. When I tried
the same on Azure I got a big error that eventually led me to find
another solution to the licensing issue and found google cloud.

## Free services

-   Compute engine: F1 + 30gb/mês
-   Cloud storage: 5gb/mês
-   BigQuery: 1tb/mês
-   Google Kubernetes Engine: 1 cluster zonal ou autopilot/mês
-   App engine: 28 instâncias/dia
-   Cloud Run: 2 milhões de solicitações/mês
-   Cloud Build: 120 minutso de compilação/dia
-   Operações: cotas mensais para geração de registros e monitoramento
-   Firestore (Banco de dados de documentos NoSQL que simplifica o
    armazenamento, a sincronização e a consulta de dados para apps): 1gb
-   Pub/Sub: 10gb/mês

[Free Trial and Free Tier  \|  Google
Cloud](https://cloud.google.com/free) [Google Cloud Platform GCP Free
Tier e Teste Gratuíto -
YouTube](https://www.youtube.com/watch?v=sAL8HlwxWMY)

## Cloud Source repositories

[Working with Cloud Source Repositories -
YouTube](https://www.youtube.com/watch?v=T_0v0DdSlLU) [Google Cloud
Platform (GCP) - Cloud Source Repositories -
YouTube](https://www.youtube.com/watch?v=ar3pEkJ1OYs)
