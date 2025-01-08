# Building Dockerfile

To make image analysis project, workflow as reproducible as possible, we create docker container for software which contains the necessary tools. Image analysis tasks usually need interactive UI, so in this excercise we use Fiji to illustrate the process.

To make things easier, the Dockerfile for Fiji is provided for this excercise. Have a look at the Dockerfile.

### Exercise 1
To build the fiji container, first go to the same location where Dockerfile located.

```
docker build -t fiji:build-01 .
```
The argument -t specify the tag of the container. You can omit the second part after ```:```, in this case, docker will use ```latest``` as the tag. 
The ```.``` is important, by default docker use Dockerfile to build the container. If the Dockerfile is located in other directory we will need the ```-f``` argument

```
docker build -t fiji:build-01 -f /path/to/dockerfile
```

Wait for the build to finish. Once the build completes, check if the images using 
```
docker images
```

### Exercise 2

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

### Exercise 3

Once the Fiji image is built, let's test it locally. Fiji is a GUI applicatin, so we need to run the container with GUI support by configuring X11 server access.

```
xhost +local:docker
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

### Excercise 4

So far we have Fiji container running locally, but what if we want to deploy it to the BARD?
Let's go back to the Dockerfile.
1. The `LABEL` in the Dockerfile are specific to the BARD. As BARD is a desktop environment, it needs to know where to show the Fiji app in BARD and what to do when users click it.
2. oc.icon and oc.icondata tells BARD which logo image to use. oc.icondata takes a base64 string for the image file fiji_icon.svg. To obtain the base64 string, we use the following
   ``` cat fiji_icon.svg |base64 ```
3. oc.cat specify which category Fiji belongs to. BARD has these categories 'Development', 'Office', 'Utilities' etc.


