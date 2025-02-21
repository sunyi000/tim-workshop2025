# Building Dockerfile

To make image analysis project, workflow as reproducible as possible, we create docker container for software which contains the necessary tools. Image analysis tasks usually need interactive UI, so in this excercise we use Fiji to illustrate the process.

To make things easier, the Dockerfile for Fiji is provided for this excercise. Have a look at the Dockerfile.

## Linux:
### Exercise 1

We start from a Dockerfile which has been prepared and will add some statements iteratively to create a valid Dockerfile for the tool Fiji.

Please have look at the Dockerfile in this repository and open the file Dockerfile. Ignore the 'Labels' for now, we will explain in much more details later.

In this example, we will start from a base image from registry.git.embl.de/grp-cbbcs/abcdesktop-apps/base-image:ubuntu22-cuda-11-8. 
You can find the Dockerfile recipe of this based image [here](https://git.embl.de/grp-cbbcs/abcdesktop-apps/-/blob/main/base-image/Dockerfile.ubuntu22-cuda-11-8?ref_type=heads).

What the user which is used in the image when tools are run?

Let's go back to the current Dockerfile and try to create Docker recipe for Fiji. 
Have a look at the [instsructions](https://imagej.net/software/fiji/downloads) for installing Fiji. Based on the explanation how to install Fiji, we create statements for this Dockerfile to install the tool.

Try to build the Docker image by adding a version tag to the build name.

```
docker build -t fiji:01 .
```

Verify if it is built successfully viwith ``` docker images ```

### Exercise 2 - Local testing

Once the Fiji image is built, let's test it locally. Fiji is a GUI applicatin, so we need to run the container with GUI support by configuring X11 server access.

```
xhost +local
```

Now Run the container 

```
docker run -it --rm -e DISPLAY=$DISPLAY -v /tmp/.X11-unix:/tmp/.X11-unix fiji:01

```

Here is the breakdown of the command
- -it runs docker container in iteractive mode.
- --rm automatically removes the container after it exits.
- -e DISPLAY=$DISPLAY sets the DISPLAY environment variable inside the container to match host computer's display
- -v mounts the X11 unix socket, allowing the container to communicate with the X server on your host.
- fiji:01 specifies the docker image to run

## MacOS

### Build container with Podman
1. Start Podman Desktop
2. Make sure Podman machine is started.
3. Once Podman machine is started, from the Podman GUI interface, click "Create". This will guide you to build a docker container.
4. Select "Containerfile or Dockerfile"
5. 'Context Path'  will be the folder which contains your Dockerfile.
6. Give your image a name.For example. test-fiji
7. For this Fiji example, leave ENV empty.
8. Click Build and wait for it to finish.
9. Once the build finishes, you should be able to see test-fiji images in your Podman desktop.

For Testing GUI container with Podman locally, you will need to install XQuartz to forward the graphical display from the container to your Mac.

#### Configure XQuartz
1. Open XQuartz from Applications > Utilities > XQuartz.
2. Go to Settings, on the Security tab, make sure "Allow connections from networkclients" is checked
3. In XQuartz, open a terminal (XQuartz terminal) window and run

` xhost + `

#### Run a GUI Container with X11
1. On Mac Terminal, Set the DISPLAY environment variable to point to your Mac’s X11 server:

`export DISPLAY=host.docker.internal:0`

This tells the container where to send the GUI output.

2. Start a GUI-based container with the proper settings:

`podman run -e DISPLAY=host.docker.internal:0 --rm `docker.io/library/test-fiji:latest `

(replace test-fiji with your own name)

The -e DISPLAY=host.docker.internal:0 tells the container where to send the GUI output.

The --rm flag removes the container after exit.

If host.docker.internal:0 doesn’t work, try:
`export DISPLAY=$(ipconfig getifaddr en0):0`






