# Simple VPS
This is the simplest possible implementation of a Virtual Private Server (VPS). It spins up
a Ubuntu-based Docker container with SSH shell access. There is no persistent storage,
so everything is held in memory and deleted if the device is rebooted. The SSH user also
does not have sudo privileges so is pretty strongly restricted in what they can do.

However, by keeping it simple, this client is preferred for testing. If you're a beginner at
setting up a P2P VPS client, you should start by following the directions below.

## Installation
These instructions assume you are starting with a fresh installation of Ubuntu 16.04 Desktop.

### Device Configuration

4. This is a great time to update the software on the device, including any security patches.
```
sudo apt-get -y update

sudo apt-get -y remove nodejs
curl -sL https://deb.nodesource.com/setup_8.x | sudo -E bash -
sudo apt-get install -y nodejs build-essential

sudo apt-get -y upgrade
```

6. You'll also need to install Docker on the RPi. Prior to running the instructions below,
this is a great time to reboot your device. It seems to prevent errors with installing Docker.

`curl -sSL https://get.docker.com | sh`

7. Follow the on-screen instructions to add the user 'pi' to the docker group.
You'll need to open a new terminal after entering this instruction:

`sudo usermod -aG docker pi`

8. Now, downgrade Docker (until they fix issues with the newer versions):

`sudo apt install docker-ce=17.09.0~ce-0~raspbian`

9. (optional) create a directory for your node applications, like this one:

`mkdir node`

10. Clone this repository:

`git clone https://github.com/P2PVPS/p2pvps-client`

11. Setup the Client program by running:
```
cd p2pvps-client
npm install
```

12. Change into the RPi simple client directory:

`cd client/rpi/simple/`

13. Install the dependencies:

`npm install`

14. Get your device GUID from the P2P VPS marketplace. This is provided in
the *Owned Devices view* by clicking the *+Add New Device* button. Paste this GUID into the `device-config.json` file.

15. Launch the simple client. The first time will take a while as it will need to download and
build several Docker containers:

`node p2p-vps-client.js`

15. Generate the files you need by running `node registerDevice.js`. Take note of the username, password, and port.

4. Build the generated Dockerfile by running the bash script `./buildImage`.

5. Run the Dockercontainer, which will establish a reverse SSH connection, by running the bash script `./runImage`.

6. You can now make an SSH connection to your Raspberry Pi by connecting to the SSH server on the port
assigned to your device in step 3, using the computer generated username and password.