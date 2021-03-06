Mulesoft Anypoint Studio ubuntu Docker edition
---

**Ubuntu version**: Desktop 20.04

**Anypoint Studio Version**: 7.5.1 (Runtime v4.3)

**Host OS**: MacOS Catalina / Windows 10

---

# Goal:

You want to, from a simple and automatic method have an virtual environment with all the tools you need to work with Anypoint Studio.


# FAQ:

 - Why not a VM?
	 - Having a fully functional VM that you can import into VMWARE or VIRTUALBOX is indeed an option but you have to have the vm file around and you need to create it, you need need to install everything. This option take that out and all you need is to run a command.

- How is the performance?
	- This "solution" will work for simple application and testing, do not think of it as a replacement.

- Does this replace installing all the software locally?
	- No, having the software installed will always be a better option, the goal here is to have a testing environment that can be quickly deployed with all the tools you need.


# How to run:

## Prerequisites:

- Sign up in [Docker Hub](https://hub.docker.com/signup) if you haven't already
- Install [Docker Desktop](https://www.docker.com/products/docker-desktop)

## Pre-check (MacOS):

 - Install [Homebrew.](https://docs.brew.sh/Installation)
 - Install **XQuartz**
   - Command: `brew cask install xquartz`
 - Install **Socat**
   - Command: `brew install socat`
- Make sure XQuartz accept client connections:
 - run the command: `open -a Xquartz`
 - On the top left menu, click on ""XQuartz" and select "Preferences"
 - On the "Security" section, be sure "Allow connections from network clients" is marked.
- Make sure socat is listening on the port 6000:
  - Command: `socat TCP-LISTEN:6000,reuseaddr,fork UNIX-CLIENT:\"$DISPLAY\"`


##  Pre-checks (windows):

- Download and install VcXsrv Windows X Server from [here](https://sourceforge.net/projects/vcxsrv/)
- Run the VcXsrv server and leave all options as default, just click next until finish.
- The VcXsrv icon is now on the windows task manager and if you hover the cursor over it, you will see your hostname and the display number, usually is zero.

## Let's give it a try:

- Download this repo and unzip it wherever you like
- From a terminal, navigate to the folder you unzipped or cloned the project.
- Build the container with the command:
	- `docker build -t <replace-with-your-docker-hub-username>/studio .`

![enter image description here](https://i.imgur.com/juJZTEw.jpg)

- Run the container with the command:

    `docker run -d -it -v [full-path-to-desktop-folder]:/root/AnypointStudio/studio-workspace -p 8081:8081 -e DISPLAY=[your-local-ip]:0 --name anypoint-studio [your-docker-hub-username]/studio`

- Accept the default workspace folder (if you change it, all changes will be lost after stop the container)
- That's it!.. have fun

MacOS:
![MacOS](https://i.imgur.com/hcYi0Bg.jpg)

Windows:
![MacOS](https://i.imgur.com/6Y5cVYA.jpg)


The docker run command above  will:
- map your **local** port 8081 to the container's port 8081.
- map your **local** desktop folder to the Container's /root/AnypointStudio/studio-workspace folder so your projects remains after you close.

- From now, all you have to do to start Studio is to run the command `docker start anypoint-studio` or starting the container from the docker dashboard, select the container and click on the "PLAY" icon.
---


In case of emergency, Nuke all local docker images and containers completely:
 - `docker system prune -a --volumes`
