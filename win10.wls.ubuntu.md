#### Ubuntu on Win10

You can now activate ubutnu WLS (windows linux subsytem) on win10

##### Ubuntu setup

Open PowerShell from 'Start' menu.
Run command

    Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux

When asked, restart Windows

##### First run and software updates

Launch your Ubuntu under Win10 from 'Start' menu. Create your default user (same as for linux account preferred) with any passowrd you wish.
This user is required for common tasks and to access root account with `sudo su -`

Check the version

    lsb_release -a

General setup

    export http_proxy=...
    export https_proxy=${http_proxy}
    echo '
     Acquire::http::Proxy "http://user:pass@server.domain.com:80";
     Acquire::https::Proxy "http://user:pass@server.domain.com:80";
    ' > /etc/apt/apt.conf.d/proxy.conf
    sudo apt update
    sudo apt install software-properties-common


Setup python installer

    apt-get install python3-pip

Add latest python versions

    add-apt-repository ppa:deadsnakes/ppa

Install general tools

    apt-get install mc 

Install tools for json

    apt-get install jq python3-demjson

Use mobaxterm to work with ubuntu console instead win10 console

Setup X-es

    echo 'export DISPLAY=:0' >> ~/.bashrc && . ~/.bashrc
    apt-get install xterm

Install java

    sudo apt install openjdk-8-jre-headless

##### Password reset

 * open regedit as admin 
 * go to Computer\HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Lxss\
 * note down the value of `DefaultUid` and set it to 0 
 * open linux wsl
 * run passwd (you are a root now)
 * close linux wsl
 * set `DefaultUid` to previous value (usually 3e8 HEX)
 * open linux wsl and `su -` to verify the change
