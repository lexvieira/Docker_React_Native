# Docker React Native
[See in English EN](README-EN.md)

Run any project with react/react native or Expo without having to install any integrated development environment (IDE) on your machine, simply using a Docker image. The only thing you will need to install is Docker on your machine, available for **Windows, Linux, Mac**. If you have never installed Docker, here is how to install [https://docs.docker.com/get-docker/](https://docs.docker.com/get-docker/).

If you want to know a little more before starting you can access this link [https://github.com/lexvieira/Docker-Init-Nodejs-React-React-Native-SQLServer](https://github.com/lexvieira/ Docker-Init-Nodejs-React-React-Native-SQLServer)

## Hands in the dough

This image is available at the link below, read on to find out how to use it.

[https://hub.docker.com/repository/docker/lexvieira/docker_react_native_deploy_01](https://hub.docker.com/repository/docker/lexvieira/docker_react_native_deploy_01)

Or just pull 👇 (download) the image.

```docker pull lexvieira/docker_react_native_deploy_01:v01```

## Dockerfile

You can also create your own image from the *Dockerfile* available in this repository.

```docker build -t drn:v01 .```

* *docker build -t drn:v01 .* -> Docker executable on Windows or Linux, where the parameter *Build ⚙️🛠️* will create an image with the following parameters

* *build -t* -> *-t* It is the parameter for the name of the *tag* or name of the image you are creating

* *drn:v01* -> In this case the image name will be: **drn:v01** (**drn** is an abbreviation for Docker React Native)

* *.* -> **.** means that you are running the command inside the folder where the **Dockerfile** is

## Post your own image and make it available online publicly or privately (if you want)

1) - Create your login on the site: [https://hub.docker.com/](https://hub.docker.com/)

2) - Log in with your account in the docker command line on Linux/Mac or through the application on Windows

```
 docker login
```

Enter username and password when prompted

3) After you've **Pull 👇** from the image or **Build ⚙️🛠️**, **Push 👆** from the image to the online repository

Example on the website [https://docs.docker.com/engine/reference/commandline/push/](https://docs.docker.com/engine/reference/commandline/push/) - Don't worry, I'll show you simple mode

```
docker tag local-image:tagname new-repo:tagname
docker push new-repo:tagname
```

Image I uploaded on [https://hub.docker.com/repository/docker/lexvieira/docker_react_native_deploy_01](https://hub.docker.com/repository/docker/lexvieira/docker_react_native_deploy_01)

```
docker tag drn:v01 lexvieira/docker_react_native_deploy_01:v01
docker push lexvieira/docker_react_native_deploy_01:v01
```

* *docker tag drn:v01* > The **tag** parameter is to identify the name of the image you created or downloaded (Pull 👇)
* *lexvieira/docker_react_native_deploy_01:v01* > is to identify where you will push 👆 your image

## Basic commands to run your projects in React / or React Native

In this link you have some basic commands to be able to run your images in a more practical way using **Alias** for example [https://github.com/lexvieira/Docker-Init-Nodejs-React-React-Native-SQLServer# using-alias-see-more-on-github-week-omnistack-10-alias-bonushttpsgithubcomlexvieiraweek-omnistack-10treerun_on_dockeralias-bonus-target_blank](Docker Alias)


* In this case I'm passing the command I use on my machine to docker my projects running a Linux Ubuntu.

### Using an Alias ​​(shortcut), to decrease the size of the commands

**Alias** is just a shortcut we created to make us type fewer commands and make our lives easier.

Below 👇 there is an **Alias** that you can either copy and paste into the terminal command line or add to your terminal configuration file **.bashrc | .zshrc** see more at the link above 👆.

**Basic commands**
```
alias drn='docker run --network host -ti -v "$(pwd)":/opt/ui -p 8081:3000 --privileged -v /dev/bus/usb:/dev/bus/usb drn: v01'
```

**Advanced command**,
1) Stop Docker if already running
2) Identifies the ip of your machine for you to run in your browser (Browser) or in your App React Native.
3) Run React Image last.
```
alias drn='$([[ $(docker container ls | grep drn:v01 | cut -d" " -f 1) != "" ]] && $(docker stop $(docker container ls | grep drn:v01 | cut -d" " -f 1)) || echo "") && ifconfig | grep inet && docker run --network host -ti -v "$(pwd)":/opt/ui -p 8081:3000 --privileged -v /dev/bus/usb:/dev/bus/usb drn:v01 '
```

No matter what shortcut you created the result will be the same, the only thing you will have to type afterwards on the command line is **drn** followed by the command you want to execute.

### In practice

First create a **folder/folder** for the project with react Native, for example `mkdir MyApp` and then run the command below
```
drn npx react-native init MyApp --template react-native-template-typescript\
```

First time running a react-native project on your Android smartphone, for **Apple** you need a Mac Book to run the project.
On Android you must enable **developer mode** (different models, different access modes), connect the **USB** cable, select **File Transfer**, after running the command below 👇 be careful to accept the **security key** when prompted, otherwise the compilation will fail. Voalá, your app is running on your cell phone. You can disconnect the **USB** and next time just run the next command.
```
drn react-native run-android
```

Last part, run your react native project to run through your machine's IP. If you don't know the IP, type `ifconfig` on **Linux**, on **Windows** `ipconfig`, and on **Mac** I have no idea (We don't know everything either 😁). Apparently it's ifconfig too.
Locate the No your App running on Android Smartphone, *shake your phone from right to left*, then select *Settings ⚙️🛠️* and then *Debug Server host & port for device*, enter the ip you received after typing *ifconfig*. Go back and click *Reload* you will notice that both on your cell phone and on your machine's terminal you will see a download percentage. And that's it, your application is live.
```
drn react-native start
```

* To run **Expo** there are some other commands to be added, I will send it in the update 😉

The **Alias**


## Updates coming ;)

Coming soon, images and more exmples

##That's all folks