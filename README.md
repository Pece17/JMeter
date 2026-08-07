# JMeter

A project for revisiting the basics of the **Apache JMeter** performance testing tool. The purpose of this project is to refresh the knowledge and skills I previously gained with **JMeter** while working as a **performance tester** several years ago.


## Table of Contents

- [Software Installation and Setup](https://github.com/Pece17/JMeter#software-installation-and-setup)
- 


## Software Installation and Setup

First I need to install the prerequisites of this project, and I start by going to https://jmeter.apache.org/download_jmeter.cgi to download the latest version (**5.6.3**) of **Apache JMeter**. I choose the **apache-jmeter-5.6.3.zip** file because I'm using **Microsoft Windows 11 Home**. There is no installation file, and instead you just **right-click** the **ZIP** file and select **Extract All...**. I'm not sure if it really matters where you place the folder, but ```C:\Tools\apache-jmeter-5.6.3``` works as a location, for example. I have it in ```C:\Users\Business\apache-jmeter-5.6.3``` because I don't use **JMeter** with my other accounts on this computer.

After that I need to install **Java** to get **JMeter** working. **ChatGPT** recommends **Eclipse Temurin** **JDK** (**Java Development Kit**) **17 -** **LTS** (**Long-term support**) because "it is one of the most commonly used **OpenJDK** distributions and works well with **JMeter**". I go to https://adoptium.net/temurin/releases?version=17&os=any&arch=any and download the **Windows** installer (**Temurin jdk-17.0.20+8, Windows 64 bit (.MSI)**). During the installation I choose **Install just for you (Business)** because I also don't use **Java** with my other accounts on this computer. Apart from that, I go with the default settings and finish the installation.

Finally, I test whether **JMeter** works by locating the **jmeter.bat** file inside the ```\apache-jmeter-5.6.3\bin``` folder. The **JMeter** application and a **terminal window** open. The **terminal** displays the following output:

```
WARN StatusConsoleListener The use of package scanning to locate plugins is deprecated and will be removed in a future release
WARN StatusConsoleListener The use of package scanning to locate plugins is deprecated and will be removed in a future release
WARN StatusConsoleListener The use of package scanning to locate plugins is deprecated and will be removed in a future release
WARN StatusConsoleListener The use of package scanning to locate plugins is deprecated and will be removed in a future release
================================================================================
Don't use GUI mode for load testing !, only for Test creation and Test debugging.
For load testing, use CLI Mode (was NON GUI):
   jmeter -n -t [jmx file] -l [results file] -e -o [Path to web report folder]
& increase Java Heap to meet your test requirements:
   Modify current env variable HEAP="-Xms1g -Xmx1g -XX:MaxMetaspaceSize=256m" in the jmeter batch file
Check : https://jmeter.apache.org/usermanual/best-practices.html
================================================================================
```

These messages are normal, and it is important not to close the **terminal window** because it will also close **JMeter**. Instead, you can **Minimize** it.

**JMeter** is now ready for use.


## Creating a Test Plan and Recording a Test Script

I now have **JMeter** opened, and it is time to create my first example **Test Plan**. **JMeter** projects are called **Test Plans**, and **Test Plan** is also always the top-level **object**. At this stage you can name your **Test Plan** as you wish. It is probably good practice to do so, so I write **Example Plan** to **Name:**.

After this I open **File** from top left corner, select **Templates...**, and choose **Recording** as my **Template** for the **Test Plan**. I click **Create** which opens a new window asking for **hostToRecord:**. I enter ```the-internet.herokuapp.com``` because it's a popular practice website for automation and testing. I leave **recordingOutputFile:** as **recording.xml** and **schemeToRecord:** as **https** because it is the right **protocol** for this website.


## Recording Test Scripts

1. open **apache-jmeter-5.6.3** folder -> **bin** -> **jmeter.bat** -> **Minimize** the terminal but don't close it
2. write **Test Plan** to **Name:**
3. click **File** -> **Save Test Plan as** -> **Save In:** to **C:\JMeter Scripts** -> write **Test Plan.jmx** to **File Name:** -> **Files of Type:** as **All Files** -> **Save**
4. click **File** -> **Templates...** -> select **Recording** -> **Create**
5. **hostToRecord:** as ```the-internet.herokuapp.com``` -> **Create**
6. select **HTTP(S) Test Script Recorder** -> **▶ Start** -> **Stop**
7. open **Google Chrome** -> **Search box** -> ```chrome://certificate-manager/``` -> **Installed by you** -> **Trusted Certificates** -> **Import** -> find **ApacheJMeterTemporaryRootCA.crt** from ```\apache-jmeter-5.6.3\bin``` -> **Open**
8. while in **Google Chrome** open **Settings** -> **System** -> **Open your computer's proxy settings** -> **Manual proxy setup** -> **Set up** -> change **Use a proxy server** as **On**, **Proxy IP address** as ```127.0.0.1```, and **Port** as ```8888``` -> **Save**
9. **HTTP(S) Test Script Recorder** -> **▶ Start** -> **Transaction name** as ```1``` for the first page -> open **Google Chrome** and ```https://the-internet.herokuapp.com/``` -> **Transaction name** as ```2```
