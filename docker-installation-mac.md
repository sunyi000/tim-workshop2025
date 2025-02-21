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
