# Before a reload
Make sure all code is pushed
Backup config files

# Just after the reload
Map library folders to OneDrive
Set scaling to 200%

# PowerShell
``` powershell
# install scoop
Set-ExecutionPolicy RemoteSigned -scope CurrentUser
iex (new-object net.webclient).downloadstring('https://get.scoop.sh')

# turn off snap assist
Set-ItemProperty -Path "HKCU:\Software\Microsoft\Windows\CurrentVersion\Explorer\Advanced" -Name SnapAssist -Value 0

# TODO add powershell script for doing nothing when lid is closed (on battery and plugged in)
# set cursor thickness
Set-ItemProperty -Path "HKCU:\Control Panel\Desktop" -Name CaretWidth -Value 3

# enable wsl
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux

# register a cmd startup script (so I can run script when a cmd shell opens)
reg add "HKCU\Software\Microsoft\Command Processor" /v AutoRun /t REG_EXPAND_SZ /d "C:\Users\jerem\OneDrive\config\init.cmd" /f

#install Docker
# TODO add script for installing docker

# install azure cli
Start-Process -PSPath "https://aka.ms/installazurecliwindows"

# install iot edge extension
az extension add -n azure-cli-iot-ext

# winget apps
winget install -e --id Docker.DockerDesktop

scoop install git
scoop bucket add extras
scoop bucket add nerd-fonts
scoop install openssh 7zip nvs jq curl python azure-cli handbrake hyper beyondcompare figlet hub kubectl helm FiraCode dotnet-sdk servicebusexplorer postman sysinternals

# TODO: setup launching of my custom profile (including hiding curl alias)

# install azcopy
(new-object System.Net.WebClient).DownloadFile("https://aka.ms/downloadazcopy-v10-windows", (Join-Path -Path $pwd -ChildPath '\azcopy.zip'))
Expand-Archive -LiteralPath azcopy.zip
# TODO: copy the binary somewhere and put it in the path

[environment]::setenvironmentvariable('GIT_SSH', (resolve-path (scoop which ssh)),'USER')

# install git-credential-manager for Windows
# not using because I believe it works to just use wincred
# (new-object System.Net.WebClient).DownloadFile("https://github.com/Microsoft/Git-Credential-Manager-for-Windows/releases/download/1.18.5/#gcmw-v1.18.5.zip", (Join-Path -Path $pwd -ChildPath '\gcmw.zip'))
# Expand-Archive -LiteralPath gcmw.zip
# ./gcmw/install.cmd
git config --global credential.helper wincred
git config --global user.name "Jeremy Foster"
git config --global user.email "jeremy.foster@live.com"
git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit --"

npm login
npm install -g typescript gitignore cowsay hexo-cli wscat2 azure-functions-core-tools jmespath json-server npm-check-updates casual lite-server speed-test yo calculator localtunnel  nodemon irish-pub @angular/cli @microsoft/rush

# install vscode (tried scoop, but vscode updates don't work)
# https://vscode-update.azurewebsites.net/latest/win32-x64-user/stable

# TODO: restore vscode config

# TODO: install VS Code extensions
mikestead.dotenv
eamodio.gitlens
ms-vscode.csharp
vsciot-vscode.azure-iot-tools
    vsciot-vscode.azure-iot-toolkit
    vsciot-vscode.azure-iot-edge
    vsciot-vscode.vscode-iot-workbench
ms-azuretools.vscode-azurefunctions
ms-kubernetes-tools.vscode-kubernetes-tools
ms-vsliveshare.vsliveshare
ryu1kn.partial-diff
shan.code-settings-sync
evilz.vscode-reveal
redhat.vscode-yaml
ms-vscode.powershell
ms-python.python
ms-vscode.cpptools
ms-azuretools.vscode-docker
ms-vscode.vscode-typescript-tslint-plugin
ms-vscode.azurecli
ms-vscode.vscode-node-azure-pack
ms-vscode-remote.remote-wsl
mhutchie.git-graph
alefragnani.Bookmarks
humao.rest-client
formulahendry.code-runner
waderyan.nodejs-extension-pack
    dbaeumer.vscode-eslint
    eg2.vscode-npm-script
    xabikos.JavaScriptSnippets
    jasonnutter.search-node-modules
    christian-kohler.npm-intellisense
    christian-kohler.path-intellisense
Mikael.Angular-BeastCode
nrwl.angular-console
alexiv.vscode-angular2-files
msjsdiag.debugger-for-chrome
anseki.vscode-color
ms-vscode-remote.vscode-remote-extensionpack
yzhang.markdown-all-in-one
streetsidesoftware.code-spell-checker
jebbs.plantuml
bencoleman.armview

//also in my install list
azure-account v0.8.7
azure-pipelines v1.157.4
azurerm-vscode-tools v0.8.3
vscode-azurefunctions v0.20.1
mssql v1.8.0
remote-containers v0.94.0
remote-ssh v0.48.0
remote-ssh-edit v0.48.0
remote-ssh-explorer v0.48.0
search-node-modules v1.3.0
team v1.161.0
vscode-aks-tools v0.0.4
vscode-apimanagement v0.1.1
vscode-azureappservice v0.16.2
vscode-azurestorage v0.7.2
vscode-cosmosdb v0.11.0
vscode-eslint v2.0.11
vscode-iot-device-cube v0.1.4
vscode-iot-workbench v0.11.0
xml v2.5.0

# Ignore irrelevant SSIDs
netsh wlan show networks | grep SSID #list them
netsh wlan add filter permission=block ssid="<Network Name>" networktype=infrastructure #ignore one


```

# Ubuntu

``` bash
sudo add-apt-repository ppa:cpick/hub #required for installing the hub package
sudo apt update
sudo apt install git p7zip-full ncdu cowsay figlet hub curl python python-pip


#install azcopy
# download tar from https://aka.ms/downloadazcopy-v10-linux
# copy it somewhere and get it in the path

# reference git-credential-manager from Windows
git config --global credential.helper store
git config --global user.name "Jeremy Foster"
git config --global user.email "jeremy.foster@live.com"
git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit --"

# install nvs and node
export NVS_HOME="$HOME/.nvs"
git clone https://github.com/jasongin/nvs "$NVS_HOME"
. "$NVS_HOME/nvs.sh" install
nvs add latest
nvs use latest

# TODO: Execute .mybashrc from .bashrc
npm login
npm install -g typescript gitignore cowsay hexo-cli wscat2 azure-functions-core-tools jmespath json-server npm-check-updates casual lite-server speed-test yo calculator localtunnel nodemon irish-pub @angular/cli @microsoft/rush

# install az cli
sudo apt-get install apt-transport-https lsb-release software-properties-common dirmngr -y
AZ_REPO=$(lsb_release -cs)
echo "deb [arch=amd64] https://packages.microsoft.com/repos/azure-cli/ $AZ_REPO main" | sudo tee /etc/apt/sources.list.d/azure-cli.list
sudo apt-key --keyring /etc/apt/trusted.gpg.d/Microsoft.gpg adv --keyserver packages.microsoft.com --recv-keys BC528686B50D79E339D3721CEB3E94ADBE1229CF
sudo apt update
sudo apt install azure-cli
az login

# install iot edge extension
az extension add -n azure-cli-iot-ext

# install azcopy
curl https://azcopyvnext.azureedge.net/release20190301/azcopy_linux_amd64_10.0.8.tar.gz -o /tmp/azcopy.tar.gz
mkdir /bin/azcopy
sudo tar -xf /tmp/azcopy.tar.gz --directory /bin/azcopy

# install kubernetes and helm
curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl
chmod +x ./kubectl
sudo mv ./kubectl /usr/local/bin/kubectl
curl -L https://git.io/get_helm.sh | bash

```

# Install from Windows Store
Ubuntu
ReddPlanet (for background changer)
Microsoft Todo
Network Speed Test
MSN Money
Kodi
Nook
Spotify
Libby
Windows DVD Player
MS Expense (link)
PureText

# Install from Web
Docker Desktop (link)
Coastal Explorer (link)
Home Designer (link)
SnagIt (link)
Office
Teams
Affinity Designer
Affinity Photo
Nitro (link)
Postman
Edge Browser (private preview)