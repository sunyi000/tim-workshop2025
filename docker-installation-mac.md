## Working with Docker on Mac ((Tested on macOS Sequoia))
We use Podman to build docker containers on Mac.

1. Download Podman Desktop from [podman.io](podman.io), and follow the instructions on screen to install it.

   You can also install podman via `brew` in terminal.
   `brew install podman`

3. After installing, create and start your first Podman machine.
   Option 1: follow the GUI instructions
   Option 2: in terminal, type the below commands
    
   ` podman machine init `
   ` podman machine start `

4. Once Podman machine is started, from the Podman GUI interface, you should see your podman machine is in 'Running' state.
6. For running GUI container with Podman, you will need to install XQuartz to forward the graphical display from the container to your Mac. 

## Install XQuarz

Since macOS does not have native X11 support, you need to install XQuartz. The installation is straightforward.

### Install XQuartz
1. Download XQuartz from xquartz.org. 
2. Install it by running the .dmg file and following the installation steps.
3. After installation, restart your Mac.
