# Project Virtual Machine
Vagrant file to build a virtual machine that can compile, test and load
all Projet required firmware.

Many thanks to the contributors of ESP open SDK & MicroPython for making their excellent software available!

# Dependencies

You must have the following software installed:

*  [VirtualBox](https://www.virtualbox.org/)
*  [VirtualBoxExtensionPack](https://www.virtualbox.org/)
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

*   and many others very important and useful tools, like ampy, pyserial, etc

## Project Compilation

You will want to first compile the ESP open SDK and MicroPython into single combined binary. Please use automator for this:

    cd ~/automator
    python automator build micropython

Compilation will take about 30 minutes to an hour or more depending on the speed of your machine.

## Connect NodeMCU to VM

To connect NodeMCU to your VM you need to update Vagrantfile with USB vendorId and producerId.
Go to host machine terminal and run:

    VBoxManage list usbhost

Now attach NodeMCU to USB port, wait for 5-10 seconds and run:

    VBoxManage list usbhost

Find new USB connection and update Vagrantfile with new device vendorId and producerId. This will look like:

    $vendor_id  = '0x10c4'
    $product_id = '0xea60'

Now, update VM with new board Id's:

    vagrant provision
    vagrant ssh
    
Check if /dev/ttyUSB0 device is present.


## Flashing ESP8266 Firmware

To flash the MicroPython firmware to the ESP8266 you can use the same automator tool:

    cd ~/automator
    python automator load micropython

## Vagrant Tips

    vagrant up - bring-up the machine
    vagrant ssh - ssh into the machine
    vagrant provision - runs the provisioning script.
    vagrant halt - shuts down the machine
    vagrant destroy - removes every trace of the machine, deletes it.
