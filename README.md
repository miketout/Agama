# Agama Desktop App
Desktop App for SuperNET DAPPs

#### For Developers
You must have `node.js` and `npm` installed on your machine.
node 9.x:
curl -sL https://deb.nodesource.com/setup_9.x | sudo -E bash -
sudo apt-get install -y nodejs

Check versions:
nodejs --version
v9.11.1

npm --version
5.6.0

Other essential dependencies:
sudo apt-get install -y build-essential

Clone Agama Desktop App with EasyDEX-GUI submodule
```shell
1) git clone https://github.com/miketout/agama --recursive --branch pkg_automation_electrum --single-branch
with this command you git clone agama - but explicitly just the pkg_automation_electrum branch (therefore --single-branch) which we also use for the release packages.
2) cd agama
3) ./binary_artifacts.sh
4) install the electron packager and prebuilt
```shell
npm install electron-packager -g
npm install electron-prebuilt -g
```
5) cd gui/EasyDEX-GUI/
Not sure step 3 is needed, works when I skipped it.
6) git checkout electrum && git pull origin electrum
7) npm install && npm install webpack webpack-dashboard
8) cd react
9) npm install
10) cd src
11) npm start
Brings up the dashboard and loads the react app using localhost:3000
12) toggle dev and debug options in settings - no idea how to do this
13) restart the app
14) sync komodod and/or asset chains - once I get the wallet running I load the chain, not sure how to do it here

You are ready to dev
```

### Important dev notes

#### Sockets.io
In dev mode backend is configured to send/receive messages from/to http://127.0.0.1:3000 address. If you open it as http://localhost:3000 sockets server will reject any messages.

#### Coin daemon binaries
Truncated instructions, we did this under step 3 above.
Run binary_artifacts.sh from under agama folder you cloned previously. The script will fetch

#### **Build the Wallet-App**
Refer to the original [electron-packager](https://github.com/electron-userland/electron-packager) repository for more detailed information.
Fairly useless advice

##### Linux
Change directory to agama and execute the following command to build the Linux app
```shell
cd agama
electron-packager . --platform=linux --arch=x64 --icon=assets/icons/agama_icons/128x128.png --out=build/ --buildVersion=0.11 --ignore=assets/bin/win64 --ignore=assets/bin/osx --overwrite
```

##### OSX
Change directory to agama and execute the following command to build the OSX app
```shell
cd agama
electron-packager . --platform=darwin --arch=x64 --icon=assets/icons/agama_icons/agama_app_icon.icns --out=build/ --buildVersion=0.2 --ignore=assets/bin/win64 --ignore=assets/bin/linux64 --overwrite
```

##### Windows
Change directory to agama and execute the following command to build the Windows app
```shell
cd agama
electron-packager . --platform=win32 --arch=x64 --icon=assets/icons/agama_icons/agama_app_icon.ico --out=build/ --buildVersion=0.2 --ignore=assets/bin/osx --ignore=assets/bin/linux64 --overwrite

# If generating 32bit desktop package
electron-packager . --platform=win32 --arch=ia32 --icon=assets/icons/agama_icons/agama_app_icon.ico --out=build/ --buildVersion=0.3 --ignore=assets/bin/osx --ignore=assets/bin/linux64 --overwrite

# To build both x64 and x86 desktop package
electron-packager . --platform=win32 --arch=all --icon=assets/icons/agama_icons/agama_app_icon.ico --out=build/ --buildVersion=0.3 --ignore=assets/bin/osx --ignore=assets/bin/linux64 --overwrite
```
change architecture build parameter to ```--arch=x64``` for 64 bit build


## Troubleshooting Instructions

### Windows DLL issues
On Windows it's noticed agama.exe complains about `VCRUNTIME140D.DLL` and `ucrtbased.dll` file.

Please see **windeps** directory and README file for instructions to install the required DLL files on Windows, and then try again running Agama App.

## Optional packages to make rpm and deb distros

electron-installer-debian

electron-installer-redhat

refer to ./make-deb.js and ./make-rpm.js
