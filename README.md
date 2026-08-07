# JMeter

A project for revisiting the basics of the **Apache JMeter** performance testing tool. The purpose of this project is to refresh the knowledge and skills I previously gained with **JMeter** while working as a **performance tester** several years ago.


## Table of Contents

- [Software Installation and Setup](https://github.com/Pece17/JMeter#software-installation-and-setup)
- 


## Software Installation and Setup

First I need to install the prerequisites of this project, and I start by going to https://jmeter.apache.org/download_jmeter.cgi to download the latest version (**5.6.3**) of the **Apache JMeter**. I choose the **apache-jmeter-5.6.3.zip** file because I'm using **Microsoft Windows 11 Home**. There is no installation file, and instead you just **right click** the **ZIP** file and select **Extract All...**. I'm not sure if it really matters where you place the folder, but ```C:\Tools\apache-jmeter-5.6.3``` works, for example. I have it in ```C:\Users\Business\apache-jmeter-5.6.3``` because I don't use **JMeter** on my other accounts on this computer.




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
