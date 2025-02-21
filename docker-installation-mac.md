## Install Docker on Mac
We use Podman to build docker containers on Mac.

1. Download Podman Desktop from [podman.io](podman.io), and follow the instructions on screen to install it.
   You can also install podman via `brew`.
   `brew install podman`

2. After installing, create and start your first Podman machine.
   ` podman machine init `
   ` podman machine start `

   You can also follow the GUI to create your first Podman machine.

3. Once Podman machine is started, from the Podman GUI interface, click "Create". This will guide you to build a docker container.
4. For running GUI container with Podman, you will need to install XQuartz to forward the graphical display from the container to your Mac.

## Install XQuarz

Since macOS does not have native X11 support, you need to install XQuartz:

### Install XQuartz
1. Download XQuartz from xquartz.org. 
2. Install it by running the .dmg file and following the installation steps.
3. After installation, restart your Mac.

## Configure XQuartz
1. Open XQuartz from Applications > Utilities > XQuartz.
2. Go to Settings, on the Security tab, make sure "Allow connections from networkclients" is checked
3. In XQuartz, open a terminal (XQuartz terminal) window and run

` xhost + `

## Run a GUI Container with X11
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

