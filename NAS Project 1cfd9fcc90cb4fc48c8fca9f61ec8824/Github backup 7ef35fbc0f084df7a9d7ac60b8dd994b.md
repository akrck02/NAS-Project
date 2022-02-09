# Github backup

I wanted  my new NAS to **create a backup of all my Github repositories locally in a regular basis** using git built in commands, so I decided to make a Javascript script on nodejs that clones the repositories and then runs **git pull** command on them 

I started setting up a new repository on github.

![Untitled](Github%20backup%207ef35fbc0f084df7a9d7ac60b8dd994b/Untitled.png)

I clone it locally using 

```bash
git clone https://github.com/akrck02/Github-backup-script
```

And enter here using

```bash
cd Github-backup-script
```

Now it’s time to set up **node** and **npm** in ubuntu.

```bash
sudo apt-get install nodejs
sudo apt-get install npm
```

## Starting the node project

I will use javascript over typescript for fast development right now, but this may be changing in the future. Let’s set up a new node project using the following command:

```bash
npm init -y
```

Then a **package.json** will be created. Now we can modify the scripts to add our service.js

```json
{
  "name": "github-backup-script",
  "version": "1.0.0",
  "description": "basic script that makes a backup of the github repositories locally,",
  "main": "service.js",
  "scripts": {
    "start": "node service.js"
  },
  "repository": {
    "type": "git",
    "url": "git+https://github.com/akrck02/Github-backup-script.git"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "bugs": {
    "url": "https://github.com/akrck02/Github-backup-script/issues"
  },
  "homepage": "https://github.com/akrck02/Github-backup-script#readme"
}
```

I didn’t change the license for this example but is highly recommendable to change it according to your license file.

I create the project directories with the following structure:

```text
/                   # our base path 
/src/               # the source code
/media/             # the files to be used by the script
```

The code is pretty simple, It uses two configuration files in json format to know the runtime parameters and the repositories to clone.

### Params.json

This json file contains the runtime parameters for the script to get the job done.

```json
{
	"directory" : "/home/nas-admin/backup",
  "interval" : "12"
}
```

### Repos.json

This one contains the repositories to be cloned and updated for each user / org. I will use a few as example, but the original file has 26+ repositories. 

```json
{
  "akrck02": [
	  "Github-backup-script",
	  "Valhalla"
	], 
	"Nightlight-studios" : ["io-world"]
}
```

## Now, let’s start coding.

Okay so we need a basic script that detects if a repository is cloned, and if it is not that executes **git clone**, and in fact if it is executes **git pull** in our established interval. I will not dive into the script itself because [you can access the code here](https://github.com/akrck02/Github-backup-script).

I created the main script of the application called **service.js** and another script called **reader.js** that reads the config files. 

Make some checking of the configuration parameters. use and interval to repeat the code, using the interval.

![Untitled.png](Github%20backup%207ef35fbc0f084df7a9d7ac60b8dd994b/Untitled%201.png)

I will improve this scheme in the future because if the net is down this may cause the script to stop, but the good idea is that is working pretty well!

### First time executing

![Untitled](Github%20backup%207ef35fbc0f084df7a9d7ac60b8dd994b/Untitled%202.png)

![Untitled](Github%20backup%207ef35fbc0f084df7a9d7ac60b8dd994b/Untitled%203.png)

### Second time executing

![Untitled](Github%20backup%207ef35fbc0f084df7a9d7ac60b8dd994b/Untitled%204.png)

![Untitled](Github%20backup%207ef35fbc0f084df7a9d7ac60b8dd994b/Untitled%205.png)
