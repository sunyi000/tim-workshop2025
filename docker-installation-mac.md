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
Step 1: Install XQuartz
Since macOS does not have native X11 support, you need to install XQuartz:

Download XQuartz from xquartz.org
Install it by running the .dmg file and following the installation steps.
After installation, restart your Mac.
Open XQuartz from Applications > Utilities > XQuartz.
Go to Settings, and on the Security tab, make sure "Allow connections from networkclients" is checked
In XQuartz, open a terminal window and run
` xhost + `

Step 2: Configure Podman Desktop for X11 Forwarding

Open Podman Desktop.
Go to Settings and make sure your Podman virtual machine is running.
Open a terminal and check if Podman is working
`podman info`

Step 3: Run a GUI Container with X11
Set the DISPLAY environment variable to point to your Mac’s X11 server:

`export DISPLAY=host.docker.internal:0`
This tells the container where to send the GUI output.
Start a GUI-based container with the proper settings:

`podman run -e DISPLAY=host.docker.internal:0 --rm `docker.io/library/test-fiji:latest `
The -e DISPLAY=host.docker.internal:0 tells the container where to send the GUI output.
The --rm flag removes the container after exit.

If host.docker.internal:0 doesn’t work, try:
`export DISPLAY=$(ipconfig getifaddr en0):0`

