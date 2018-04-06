# Project Virtual Machine
Vagrant file to build a virtual machine that can compile, test and load
all Projet required firmware.

Many thanks to the contributors of ESP open SDK & MicroPython for making their excellent software available!

# Dependencies

You must have the following software installed:

*  [VirtualBox](https://www.virtualbox.org/)
*  [Vagrant](https://www.vagrantup.com/)

# Usage

Clone this repository and navigate to it in a command terminal, then run the following command to bring the Vagrant virtual machine up and provision it for compiling the tools:

    vagrant up

After the virtual machine is brought up and provisioned use the following
command to enter an SSH session on it:

    vagrant ssh

Once inside the virtual machine you will see two git repositories that have
already been cloned:

*   [esp-open-sdk](https://github.com/pfalcon/esp-open-sdk) - This is an SDK to compile code for the ESP8266's processor.

*   [micropython](https://github.com/ykholod/micropython) - This is the MicroPython SDK which allows running embedded Python code on an ESP8266.

*   [automator](https://github.com/ykholod/automator) - This is the automation suite to build, validate and load Project firmware

*   [esptool](https://github.com/themadinventor/esptool) - This python script flashes ESP8266 ASIC with custom image.

## Project Compilation

You will want to first compile the ESP open SDK and MicroPython into single combined binary. Please use automator for this:

    cd ~/automator
    python automator build micropython

Compilation will take about 30 minutes to an hour or more depending on the speed of your machine.

## Stopping & Starting the VM

To stop the VM make sure you've exited from any SSH session on it (run the `exit`  command) and then run this command inside the directory with the Vagrantfile:

    vagrant halt

To start the VM and SSH into it again just run:

    vagrant up
    vagrant ssh

## Flashing ESP8266 Firmware

To flash the MicroPython firmware to the ESP8266 you can use the same automator tool:

    cd ~/automator
    python automator load micropython

