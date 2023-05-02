Download Link: https://assignmentchef.com/product/solved-cpe459-exercise1-getting-started-with-scada
<br>
This exercise has two parts.

<ol>

 <li>Install software to use OpenPLC. You will install and configure:

  <ol>

   <li>Two virtual machines with Ubuntu Desktop LTS.</li>

   <li>Moba Xterm.</li>

   <li>OpenPLC runtime.</li>

   <li>OpenPLC Editor.</li>

   <li>Arduino IDE.</li>

   <li>SCADABr Human Machine Interface (HMI) software.</li>

  </ol></li>

 <li>Design ladder logic and implement logic circuitry for your first SCADA system.</li>

</ol>




<h1>2         Part 1: Installing Software</h1>

<h2>2.1        Virtual Box VMs</h2>

<ol>

 <li>Download and install the Oracle Virtual Box.Link: <a href="https://www.virtualbox.org/wiki/Downloads">https://www.virtualbox.org/wiki/Downloads</a>Select the link that matches your operating system (Windows, MAC, Linux).Run the downloaded executable and accept all defaults.You may need to reboot your computer.</li>

 <li>Download and install the extension pack.</li>

</ol>

Link: <a href="https://www.virtualbox.org/wiki/Downloads">https://www.virtualbox.org/wiki/Downloads</a>

Click the link under “VirtualBox 6.1.16 Oracle VM VirtualBox Extension Pack

Clink on the downloaded file, in Explorer or in your browser, and follow directions to install.

2.2        Install Ubuntu Desktop LTS

<ol>

 <li>Download an Ubuntu Desktop LTS .iso file.</li>

</ol>

Link: <a href="https://ubuntu.com/download/desktop">https://ubuntu.com/download/desktop</a>Click the Download link to download. The file is quite large (2GB+). It will take a while to download.  Coffee break &#x1f60a;

<ol start="2">

 <li>Install the .iso within VirtualBox.</li>

 <li>Open the Oracle VirtualBox VM Manager.</li>

 <li>Press <em>New</em></li>

 <li>Name the new VM <em>PLC</em></li>

 <li>Change the type to Linux</li>

 <li>Select Defaults for Memory Size, Hard Disk, Hard disk file type, Storage on physical hard disk, File location and size.</li>

 <li>Your VM is now created, but we still must install the OS on the VM.</li>

 <li>Within the Oracle VirtualBox VM Manager, select the PLC VM, and then click Settings.</li>

 <li>Click Storage.</li>

 <li>Under Controller IDE select the DVD symbol.</li>

 <li>On the far right click the DVD symbol and select <em>Choose a disk file</em>.</li>

 <li>Select the .iso file downloaded from the Ubuntu website.</li>

 <li>Start the VM and follow install instructions within the Ubuntu OS.</li>

 <li>Remove the .iso from the VM DVD drive.</li>

 <li>Reboot your PLC VM (this new VM).</li>

 <li>Configure to turn off the desktop (GUI) environment.We will run with command line to conserve computer resources.</li>

</ol>

Link: <a href="https://linuxconfig.org/how-to-disable-enable-gui-on-boot-in-ubuntu-20-04-focal-fossa-linux-desktop">https://linuxconfig.org/how-to-disable-enable-gui-on-boot-in-ubuntu-20-04-focal-fossa-linux-desktop</a>

Open a terminal.

Enter command <em>sudo systemctl set-default multi-user</em>

Enter command <em>shutdown -r </em>to reboot.




<h2>2.3        Clone the PLC Linux to create a second VM for your HMI.</h2>

In the Oracle VM VirtualBox Manager

Select and highlight the PLC VM

Right click and select Clone

Set the name to <em>HMI </em>then click Next

Select Linked clone then click Clone

<h2>2.4        Install OpenPLC runtime in the PLC VM</h2>

Link: <a href="https://www.openplcproject.com/runtime/linux/">https://www.openplcproject.com/runtime/linux/</a>

git clone https://github.com/thiagoralves/OpenPLC_v3.git

cd OpenPLC_v3

./install.sh linux




Use command <em>ip a</em> to note your VM’s IP address.

The OpenPLC runtime starts automatically whenever your VM boots.




Create a network proxy to access the OpenPLC runtime from your host’s browser.

In the Oracle VM VirtualBox Manager

Select the PLC VM

Click settings and select Network

Under Adapter 1, Advanced, click port forwarding.

Add a rule to forward port 8080 from the PLC VM to port 8000 on the host.

Then in your browser navigate to <a href="http://localhost:8000">http://localhost:8000</a> (This webpage is the control interface for your PLC)

<em>Note: you may need to reboot the VM for the proxy to take effect.</em>




<h2>2.5        Install MobaXterm</h2>

Link: <a href="https://mobaxterm.mobatek.net/download.html">https://mobaxterm.mobatek.net/download.html</a>

Download the installer application.

Run the installer.

Open the MobaXterm application.

Click <em>Start local terminal</em>.

Record the IP address provided in the local terminal. This will be used when starting GUI applications in VM’s.




<h2>2.6        Install the OpenPLC editor in the PLC VM</h2>

Link: <a href="https://www.openplcproject.com/plcopen-editor/">https://www.openplcproject.com/plcopen-editor/</a>

sudo apt-get install git

git clone https://github.com/thiagoralves/OpenPLC_Editor

cd OpenPLC_Editor

./install.sh

To start the OpenPLC Editor:

Open a terminal in the VM.

Use the command: <em>DISPLAY=192.168.86.63:0.0 plcopeneditor&amp;</em>

Note: replace the IP address above with the IP address from Mobaxterm




<h2>2.7        Install the Arduino IDE in the PLC VM</h2>

Link: <a href="https://www.arduino.cc/en/guide/linux">https://www.arduino.cc/en/guide/linux</a>

In your PLC VM, download https://downloads.arduino.cc/arduino-1.8.13-linux64.tar.xz

Uncompress the IDE installer (tar -xvf arduino-1.8.13-linux64.tar.xz)

cd Downloads/Arduino-1.8.13

./install.sh

DISP

To run: DISPLAY=192.168.86.63:0.0 arduino&amp; (a window will open on the host PC)

<em>Note: replace the IP address above with the IP address from Mobaxterm</em>




<h2>2.8        Install SCADABr in the HMI VM</h2>

Link: https://www.openplcproject.com/reference/scadabr/

git clone https://github.com/thiagoralves/ScadaBR_Installer.git

cd ScadaBR_Installer

./install_scadabr.sh

To open SCADABr on a browser (option 1):

Open a terminal in the VM.

Use the command: <em>DISPLAY=192.168.86.63:0.0 firefox&amp;</em>

<em>Note: replace the IP address above with the IP address from Mobaxterm</em>

<em> </em>

Navigate to <a href="http://localhost:9090/ScadaBR">http://localhost:9090/ScadaBR</a>

<em>Note: you may need to reboot the VM for the proxy to take effect.</em>




To start the OpenPLC Editor (option 2):

Create a port forwarding rule to map VM port 9090 to host port 9000.

In your host’s browser Navigate to <a href="http://localhost:9000/ScadaBR">http://localhost:9000/ScadaBR</a>




Note: There may be problems with the apache server.

Navigate to the tomcat directory (<em>cd /opt/tomcat6/apache-tomcat-6.0.53/</em>).

<em>cd logs</em>

<em>cat catalina.out | less</em> (look for SEVERE)

restart apache (<em>sudo /opt/tomcat6/apache-tomcat-6.0.53/bin/startup.sh</em>)




<h2>2.9        Linux Command Line tips:</h2>

<ol>

 <li>Set your display for MOBAXTERM.</li>

</ol>

Use <em>export DISPLAY=192.168.1.1:0.0</em>

Change the IP address above to match your MOBAXTERM IP address. Start a local terminal in MOBAXTERM to find your MOBAXTERM IP address.




<ol start="2">

 <li>Shutdown a Linux VM with the <em>shutdown now </em></li>

 <li>Reboot a Linux VM with the <em>shutdown now -r</em> command</li>

 <li>Capture or release mouse (move mouse control from VM to host or host to VM).

  <ol>

   <li>Press the capture key. This is the right CTRL key by default.</li>

  </ol></li>

</ol>




<h1>3         Part 2: Creating your first OpenPLC Project</h1>

Follow directions from the OpenPLC Project webpage to build your first project.

Review the material at the links below for background information needed to complete this exercise.

<ul>

 <li><a href="https://www.openplcproject.com/reference/basics/what-is-a-plc">What is a PLC?</a></li>

 <li><a href="https://www.openplcproject.com/reference/basics/introduction-to-ladder-logic">Introduction to Ladder Logic</a></li>

 <li><a href="https://www.openplcproject.com/reference/basics/contact">Contact</a></li>

 <li><a href="https://www.openplcproject.com/reference/basics/coil">Coil</a></li>

</ul>




Using the Arduino kit provided, follow the instructions at the link below to build the circuit shown and then create ladder logic to run on your OpenPLC.

Link: <a href="https://www.openplcproject.com/reference/basics/first-project">https://www.openplcproject.com/reference/basics/first-project</a>

Figure 1: Circuit for First

Additional Information:

<ol>

 <li>Refer to slide deck 03-04-Boarding_C.pptx for more information.

  <ol>

   <li>Arduino pinout: Slides 15-16</li>

   <li>Arduino to OpenPLC V3 pin name conversion: Slide 8</li>

   <li>Resistor sizes via color bands: Slide 20</li>

   <li>Switch orientation: Slides 21-22</li>

   <li>LED pin orientation: Slide 25</li>

  </ol></li>

 <li>The figure shows a generic OpenPLC. You are connecting to pins on the Arduino Uno.</li>

 <li>There is no resistor shown before between the LED and the PLC. Add one to avoid burning your LED. Use between a 1K – 10K ohm resistor. The lower the resistance the brighter the LED.</li>

 <li>R1 and R2 are pull down resistors. All input pins that you use should have a pull down resistor between 1K and 10K ohms. Note: without the pull down the pin will “float”. This will cause unpredictable behavior which is unpredictable and therefore hard to debug.</li>

 <li>The pin numbers for Arduino Uno are slightly different. Use %IX100.0, %IX100.1 and %QX100.0 (use these values in the OpenPLC editor).</li>

 <li>There is additional pin mapping information for Arduino here: <a href="https://www.openplcproject.com/runtime/arduino/">https://www.openplcproject.com/runtime/arduino/</a>. This maps the %IX100.0, %IX100.1 and %QX100.0 values from Figure 1 to Arduino pin numbers.</li>

</ol>

<h1>4         Post Exercise Report</h1>

<ol>

 <li>Which machine (virtual or physical) serves as the PLC for the SCADA project completed in part 2? In other words where is the microprocessor that implements the PLC?</li>

 <li>Which machine (virtual or physical) serves as an input/output board to connect the PLC to the physical system implemented in part 2?</li>

 <li>Describe the steps to observe the value of a switch on the breadboard. What occurs at the switch, the Arduino, PLC, network, and HMI? What order does this occur?</li>

 <li>Describe the steps to turn on a LED on the breadboard. What occurs at the switch, the Arduino, PLC, network, and HMI? What order does this occur?</li>

</ol>














