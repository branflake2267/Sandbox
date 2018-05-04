# Sencha Architect
Rapidly create rich Ext JS interfaces with Sencha Architect.
Sencha Architect is a desktop application that helps you create interfaces faster than ever in an easy-to-use, drag-and-drop environment.

## Project Dependencies

 * electron (private)
 * electron-modules
 * electron-packager
 * asar
 * nodejs
 * nodejs packages: electron-packager, asar
 * ruby
 * ruby gems: sass 3.2.13, compass 0.12.2, compass-colors, compass-recipes
 * Sencha Cmd ([6.5.0.180](https://teamcity.sencha.com/viewLog.html?buildId=610248&tab=artifacts&buildTypeId=Cmd_65x_Continuous#!29lr) or higher)
 * openjdk-8-jre 
 * p7zip-full
 * install4j
 * xvfb (just only on headless server)

## Teamcity

* [Teamcity Architect Project](https://teamcity.sencha.com/project.html?projectId=Architect)


## Building
Use this configuration to compile the build.

### Working Directory
Create the project in the home directory under work.
After this configuration is complete, you could rename the `~/work` directory.

	mkdir -p ~/work/repo
	cd ~/work

### Clone
Clone thsese github projects into `~/work/repo`.

	git clone --recursive https://github.com/extjs/SenchaDesigner.git ~/work/repo/architect
	git clone https://github.com/extjs/SenchaDesigner-binaries.git ~/work/repo/architect-binaries

### Checkout
Checkout the github master branch.

	cd ~/work/repo/architect
	git checkout 4.x

### Build Script
Build for Architect 4.2.0.666 with electron 1.6.2

	touch ~/work/build.sh
	gedit ~/work/build.sh

```
#!/bin/sh
# ~/work/build.sh
# Debugging version below.

export ASAR_ENCRYPT="false"
export ASSETS_BUILD_ALWAYS="false"
export ASSETS_INCLUDE_IN_APP="false"
export BUILD_NUMBER="100"
export BUILD_TARGETS="linux-x64"
export CHANNEL="4.2-nightly"
export DEBUG="true"
export DEPLOY="false"
export DISABLE_TESTS="false"
export ELECTRON_VERSION="1.6.2"
export PRODUCE_APP="false"
export PRODUCE_INSTALLER="false"
export PRODUCE_INSTALLER_ASSETS="false"
export PRODUCE_SRC="false"
export PRODUCE_UPDATES="false"
export SHOW_DEV_TOOLS="true"
export SIGN_EXECUTABLES="false"
export CODE_SIGN_URL_MACOS="http://172.16.1.211:8080/sign"
export CODE_SIGN_URL_WINDOWS="http://10.106.4.2:8080/sign"
./repo/architect/scripts/build/architect.sh
```

### Executable
Change the file permissions so the sh files are executable.

	chmod +x ~/work/repo/architect/scripts/build/architect.sh ~/work/build.sh

### Create Directories
Create these folders in the `~/work/assets` folder. 

	cd ~/work
	mkdir assets \
	assets/ext42 \
	assets/ext50 \
	assets/ext51 \
	assets/ext60 \
	assets/ext62 \
	assets/ext65 \
	assets/cmd \
	assets/electron-modules \
	assets/electron-binaries

### Downloads
Download these dependencies into the` ~/work/assets` directory.

* download [ext-4.2.1-commercial.zip](https://teamcity.sencha.com/viewLog.html?buildId=170781&buildTypeId=bt160&tab=artifacts) to assets/ext42
* download [ext-5.0.1-commercial.zip](https://teamcity.sencha.com/viewLog.html?buildId=223462&buildTypeId=Sencha5_50Distribution&tab=artifacts#!epgs1v7r4o) to assets/ext50
* download [ext-5.1.4-commercial.zip](https://teamcity.sencha.com/viewLog.html?buildId=583693&buildTypeId=Sencha5_50Distribution&tab=artifacts#!epgs1v7r4o) to assets/ext51
* download [ext-6.0.2-commercial.zip](https://teamcity.sencha.com/viewLog.html?buildId=495021&buildTypeId=Sencha6_60Distribution&tab=artifacts#!epgs1v7r4o) to assets/ext60
* download [ext-6.2.1-commercial.zip](https://teamcity.sencha.com/viewLog.html?buildId=567701&buildTypeId=Framework_61_Distribution&tab=artifacts#!epgs1v7r4o) to assets/ext62
* download [ext-6.5.0-commercial.zip](https://teamcity.sencha.com/viewLog.html?buildId=611440&buildTypeId=Framework_65_Distribution&tab=artifacts#!epgs1v7r4o) to assets/ext65
* download [SenchaCmd-6.5.0.180-universal.zip](https://teamcity.sencha.com/viewLog.html?buildId=610248&buildTypeId=Cmd_65x_Continuous&tab=artifacts#!29lr) to assets/cmd
* download [electron-1.6.2 folder for macOS](https://teamcity.sencha.com/viewLog.html?buildId=609199&tab=artifacts&buildTypeId=ElectronModules_OsxContinuous) to assets/electron-modules
* download [electron-1.6.2 folder for Linux](https://teamcity.sencha.com/viewLog.html?buildId=609197&tab=artifacts&buildTypeId=ElectronModules_Continuous) to assets/electron-modules
* download [electron-1.6.2 folder for Windows](https://teamcity.sencha.com/viewLog.html?buildId=609198&tab=artifacts&buildTypeId=ElectronModules_WindowsContinuous) to assets/electron-modules
* download [electron-v1.6.2-darwin-x64.zip](https://teamcity.sencha.com/viewLog.html?buildId=613363&tab=artifacts&buildTypeId=ElectronPrivate_OsxNightly) to assets/electron-binaries
* download [electron-v1.6.2-linux-ia32.zip](https://teamcity.sencha.com/viewLog.html?buildId=613365&tab=artifacts&buildTypeId=ElectronPrivate_LinuxNightly) to assets/electron-binaries
* download [electron-v1.6.2-linux-x64.zip](https://teamcity.sencha.com/viewLog.html?buildId=613365&tab=artifacts&buildTypeId=ElectronPrivate_LinuxNightly) to assets/electron-binaries
* download [electron-v1.6.2-win32-ia32.zip](https://teamcity.sencha.com/viewLog.html?buildId=613374&tab=artifacts&buildTypeId=ElectronPrivate_WindowsNightly) to assets/electron-binaries
* download [electron-v1.6.2-win32-x64.zip](https://teamcity.sencha.com/viewLog.html?buildId=613374&tab=artifacts&buildTypeId=ElectronPrivate_WindowsNightly) to assets/electron-binaries
* download [encrypter](https://teamcity.sencha.com/viewLog.html?buildId=613365&buildTypeId=ElectronPrivate_LinuxNightly&tab=artifacts#!ilqo8x7w0) to assets/electron-binaries/encrypter/encrypter

* download [install4j_linux_6_1_5.deb](https://www.ej-technologies.com/download/install4j/files) to ~/Downloads

### Install Install4j
Install Install4j and add the sencha license to it. 

* Goto the site and download Install4j https://www.ej-technologies.com/download/install4j/files 
* Load up the application.
* Add install4j/bin to the PATH.
* Old configuration.

		cd ~/Downloads
		sudo dpkg -i ~/Downloads/install4j_linux_6_1_5.deb
		sudo apt-get install -y openjdk-8-jre
		install4jc -L L-M6-SENCHA#50032550020001-yh3jia2yiz83td#35b8

### Install Dependencies
Install these dependencies. 

	cd ~
	sudo apt-get install p7zip-full
	sudo apt-get install -y ruby
	sudo gem install sass --version 3.2.13
	sudo gem install compass --version 0.12.2
	sudo gem install compass-colors
	sudo gem install compass-recipes

	curl -sL https://deb.nodesource.com/setup_7.x | sudo -E bash -
	sudo apt-get install -y nodejs

	sudo npm install -g asar
	sudo npm install -g electron-packager

### Sencha CMD 
Make sure you have the appropriate version of Sencha Cmd on your path.

	cd ~
	sencha --version

### Building
Run the build with `~/work/build.sh`. 
This will prep for debugging. 

	cd ~/work
	./build.sh


## Debugging

### Build
Start with building it first. 

### Electron Path
Add electron to the path

	# ~/.profile
	# PATH="$PATH:/home/parallels/work/assets/electron-binaries/electron" # <- example
	PATH="$PATH:[replace this with ~]/work/assets/electron-binaries/electron"
	
### Running Debugging
This will launch the electron application.

	cd ~/work/assets/electron-binaries/electron
	electron .

