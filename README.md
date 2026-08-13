# JMeter

A project for revisiting the basics of the **Apache JMeter** performance testing tool. The purpose of this project is to refresh the knowledge and skills I previously gained with **JMeter** while working as a **performance tester** several years ago.


## Table of Contents

- [Software Installation and Setup](https://github.com/Pece17/JMeter#software-installation-and-setup)
- [Creating a Test Plan and Recording a Test Script](https://github.com/Pece17/JMeter/blob/main/README.md#creating-a-test-plan-and-recording-a-test-script)
- [Recording and Correlating a Test Script with a Dynamic Token](https://github.com/Pece17/JMeter/blob/main/README.md#recording-and-correlating-a-test-script-with-a-dynamic-token)


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

I now have **JMeter** opened, and it is time to create my first example **Test Plan**. **JMeter** projects are called **Test Plans**, and **Test Plan** is also always the **top-level element**.

I start by opening **File** from the top-left corner, selecting **Templates...**, and choosing **Recording** as my **Template** for the **Test Plan**. I click **Create**, which opens a new window asking for **hostToRecord:**. I enter ```the-internet.herokuapp.com``` because it's a popular practice website for automation and testing. I leave **recordingOutputFile:** as ```recording.xml``` and **schemeToRecord:** as ```https``` because it is the correct **protocol** for this website. Then I press **Create** again. The **hostToRecord:** address is automatically applied to **elements** like **User Defined Variables** and **HTTP Request Defaults**, which is very convenient.

At this stage you can name your **Test Plan** as you wish. It is probably good practice to do so, so I select **Test Plan** and enter ```Example Plan``` into the **Name:** field. Now is also a good time to save, so I open **File** again, select **Save Test Plan as**, choose the destination, leave ```Example Plan.jmx``` as the **File Name:**, and **Save**. I save my **JMeter test plans** to ```C:\Users\Business\JMeter Scripts```, but the location is personal preference.

Next up, I select the grayed out **element** called **HTTP(S) Test Script Recorder** and press **▶ Start**. This opens a window notifying about a **certificate** being created. I press **OK** and another window called **Recorder: Transactions Control** opens. I press **❌ Stop** because I first need to **import** the new **certificate** into the **web browser** I'll be using for recording. I have decided to use **Google Chrome** for recording because it is not my main browser and I have cleared its **browsing data**.

I open **Google Chrome** and paste ```chrome://certificate-manager/``` into the **address bar**. I then click **Installed by you** under **Custom**, select **Import** next to **Trusted Certificates**, locate the **ApacheJMeterTemporaryRootCA.crt** **certificate** in ```\apache-jmeter-5.6.3\bin``` location, and press **Open**. The following text appears:

```
_ JMeter Root CA for recording (INSTALL ONLY IF IT S YOURS)
```

Remaining in **Google Chrome**, I open the **three-dot menu** from the top-right corner, open **Settings**, open **System**, and select **Open your computer's proxy settings**. This opens the **Proxy** settings in **Windows 11**. I press **Set up** under **Manual proxy setup**, turn **Use a proxy server** as **On**, enter ```127.0.0.1``` as the **Proxy IP address**, enter ```8888``` as the **Port**, and press **Save**.

- ```127.0.0.1``` is the **loopback address**, meaning it points back to your own computer. It is commonly used as the equivalent of **localhost**.
- ```8888``` is the **port number** where **JMeter**'s **HTTP(S) Test Script Recorder** listens for **proxy connections**.

Now I can start the actual recording part after my configured **proxy** has been turned on. It is worth noting that when this **proxy** is on, you cannot use internet regularly, but you only need the **proxy** on during the **recording phase**. I go back to **JMeter** and **HTTP(S) Test Script Recorder**, press **▶ Start**, and enter ```1``` as the first **Transaction name** in the **Recorder: Transactions Control**. I think this is a good way to identify every action during the recording, because there can be multiple **samplers** per action. Later you can name the **transactions** more descriptively, if you wish. In **JMeter**, a **sampler** is the component that actually sends a request or performs an action and records the response. It is also very important to determine carefully what actions you will be taking during a recording of a script. In real-life situations you would usually determine the actions of a **test case**, like a **script**, together with the **client**. For example: go through this specific sequence on a website, click these pages, log in with these credentials, etc.

I will determine a very simple **test case** for my first **script**, because I really just want to see if **JMeter** recording is working correctly.

1. Enter the https://the-internet.herokuapp.com/ address.
2. Click **Basic Auth** link.
3. Enter **Username** and **Password** (both are **admin**), and click **Sign in**.

After signing in, no more actions during this recording, but there is a greeting message (**Congratulations! You must have the proper credentials.**) that we can later use to check whether the script can access this page. All in all, **3** **transactions**.

At this point I remembered something important. Before recording, I'm going to exclude some **URL patterns**, like **Google's services**, since I don't want to test those. I go to **HTTP(S) Test Script Recorder**, open the **Requests Filtering** tab, and **Add** or **Add from Clipboard** ```android\.clients\.google\.com.*``` and ```www\.google\.com.*``` under **URL Patterns to Exclude**. These use **regular expressions** (**regex**) that are patterns that describe what text you want to find or match. For example:

- ```\.``` = a literal dot
- ```.*``` = any number of any characters

I will return to the topic of **regex** later during this project.

Back to the recording: I managed to seemingly successfully record the previously determined **test case**, and the **script** looks clean since I excluded the unwanted **URL patterns**. In **JMeter** under the **element** called **Recording Controller**, you can see in real time when **Transaction Controllers** are created during recordings. Under **Transaction Controllers** there can be elements like **HTTP Requests** and **HTTP Authorization Managers**, among many others. I have **three** **Transaction Controllers** named ```1```, ```2```, and ```3```, so now it's easy to remember what each of those do.

Now I can test if my script works, and in theory it should because there aren't any **dynamic values** present in this script. I open a **listener** called **View Results Tree** under an **element** called **Thread Group**. It lets you inspect the results of individual **samplers** in a test. In **JMeter** there is the **toolbar** on top of the user interface, and I press the **▶** (**Start**) button to run my script while having the **View Results Tree** open. All **samplers** return **green check marks** (**✅**), which indicates that the **requests** are succeeding. But if we really want to be sure that the script is visiting all the correct pages, we can add **elements** called **Response Assertions** under **Transaction Controllers** after **samplers**. Since this script only visits **2** different pages, I will only add **Response Assertions** under ```1``` and ```2``` **Transaction Controllers**. You simply **right-click** a **Transaction Controller**, hover over **Add**, hover over **Assertions**, and select **Response Assertion**. You can do the same to other **Transaction Controllers** or just **copy and paste** the element into them.

I open the first **Response Assertion** and **Add** text ```Welcome to the-internet``` under **Patterns to Test**. I don't touch other settings. To the second **Response Assertion** I add the previously noticed text ```Congratulations! You must have the proper credentials.```. I clear the previous **View Results Tree** results by pressing the **gear and broom** (**Clear**) icon in the **top toolbar**, and I run the script again successfully. You can even test what happens if an **assertion** fails by purposely writing a wrong text into a **Response Assertion**.

> Once a **test script** has been recorded, the **HTTP(S) Test Script Recorder** can be deleted from a **Test Plan**, as it is **only needed during the recording process**. However, **it is not absolutely necessary** because the **HTTP(S) Test Script Recorder** is **Disabled** by default. You can **Disable** and **Enable** the **Elements** in **JMeter** by **right-clicking** on them and selecting **Disable** or **Enable**. This can be useful if you want to **disable** certain **HTTP Requests** without deleting them, for example.

This is now a simple, working **JMeter** script. Of course, we are only using **1 Thread** or **Vuser** (**virtual user**), which can be seen by selecting **Thread Group**. The **key settings** you can configure in this **element** are:

- **Number of Threads (users):**
- **Ramp-up period (seconds):** = how quickly **JMeter** starts all the **threads** (**Vusers**) in a **thread group**. For example, **100 virtual users** + **100-second ramp-up** = approximately **1 Vuser started per second**.
- **Loop Count:** = how many times a **Vuser** will run the script. For example, if you have **2 Vusers** and **Loop Count** set to **2**, the script will be executed **4 times in total**. The **Loop Count** can also be set to **Infinite**, meaning the script will, in theory, **run indefinitely**.
- **Same user on each iteration** = determines whether **Vusers** are reused between **iterations** or treated as **new users**.

For the scope of this project, though, I am not going to delve more deeply into how actual **performance tests** are configured. At least not at this stage. The main focus of this project is to get the scripts running with **1 or a few Vusers** at most. This reflects the **real-life workflow**: you don't perform an **actual performance test** until the scripts have been **verified to work**.

This concludes this chapter about **creating a Test Plan** and **recording a Test Script**.


## Recording and Correlating a Test Script with a Dynamic Token

I want to up the difficulty for my next example **JMeter script**, and I'm specifically interested in **dynamic tokens**. A **dynamic token** is a value that is generated or changes during a session or request flow, instead of being **static** or **unchanging**. In the upcoming example, the **dynamic token** is an **XSRF token**, which is used as a security measure to help protect against **cross-site request forgery** (**CSRF**) attacks. Per [Wikipedia](https://en.wikipedia.org/wiki/Cross-site_request_forgery), **CSRF** is a type of **malicious exploit** of a website or web application where **unauthorized commands** are submitted from a user that the web application trusts. **CSRF** and **XSRF** are two names for the same type of attack, and **XSRF**/**CSRF tokens** are a defense against that attack.

For this exercise I'm using the following website: https://authenticationtest.com/. I will determine the **steps** of this **test case** at this point, before creating a new **JMeter Test Plan**:

1. Enter the https://authenticationtest.com/ address.
2. Click the **XSRF Challenge** button under **Challenges**.
3. Enter the **E-Mail Address** (```xsrf@authenticationtest.com```) and **Password** (```pa$$w0rd```), do not touch the **XSRF Token**, and click **Log In**.
4. Verify success by seeing **Login Success** and a **longer message**, and click **Sign Out**.
5. Verify that you have returned to the starting page (https://authenticationtest.com/).

In actuality, there will only be **4 transactions** in this recording.

I open **JMeter** and create a new **Recording** template using ```authenticationtest.com``` as the **hostToRecord** and ```https``` as the **schemeToRecord**. I name the **Test Plan** as **XSRF_Plan** and save this **XSRF_Plan.jmx** file to my regular destination. Before recording, I exclude the following **URL patterns** to avoid cluttering my script:

- ```android\.clients\.google\.com.*```
- ```www\.google\.com.*```
- ```android\.clients\.google\.com.*```
- ```content-autofill\.googleapis\.com.*```


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
