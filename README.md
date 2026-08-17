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
- ```content-autofill\.googleapis\.com.*```
- ```passwordsleakcheck-pa\.googleapis\.com.*```

> It is good practice to do a few "**dry runs**" with the **HTTP(S) Test Script Recorder** before recording the final "product", because you can check which unnecessary **URL patterns** should be excluded, and you will be more confident in executing the **test case** correctly.

After a few **dry runs**, I'm ready to record the actual script, so I **Remove** all the practice **Transaction Controllers** under **Recording Controller**, **delete the browsing data** of **Google Chrome** just in case, and turn on my **proxy server**.

The recording goes smoothly. I play the script a few times, and there aren't any apparent errors, but **this doesn't mean the script is working properly yet**. In fact, it would be problematic if it worked properly because I have not **correlated** the **dynamic XSRF token** yet.

**Correlation** is the process of **extracting a dynamic value** from a **previous response** and **reusing it in a later request**. In this example, **JMeter** must **extract** the dynamically generated **XSRF token** from the **XSRF Challenge page's response** and then use that same **token** when sending the **login request**.

The first modification I will make to the script is to add **4 Response Assertions**, with **1** inside each **Transaction Controller**. This way I can actually **verify** whether all the **expected pages are loading correctly**.

1. **Response Assertion** = ```A simple playground for developers and security engineers```
2. **Response Assertion** = ```Forge Ahead!```
3. **Response Assertion** = ```You will be logged in for the next 10 minutes.```
4. **Response Assertion** = ```A simple playground for developers and security engineers```

> In **View Results Tree**, you can use the **Search** function to find which **Samplers** (in this case, **HTTP Requests**) contain the **text you are looking for**. There are also options for **Case sensitive** and **Regular exp.** searches. After this, you can use the **Find** function within each **Sampler** to **locate the exact position** of the **text you are looking for**, which can be useful when creating **Response Assertions**. Alternatively, you can **right-click** and select **View page source** (or press **Ctrl+U**) in your **web browser** to look for the **text you want to use** in a **Response Assertion**.

Now when I run the script, all the **Response Assertions** fail, which is actually surprising because it means even the **first page** (https://authenticationtest.com/) in my **test case** is **not returning** the expected, readable **Response Body**. I open **View Results Tree**, select the **HTTP Request** that **loads the first page**, and select **Response Body** under the **Response data** tab. For some reason, I was unable to copy all of the content within the **Response Body**, but it just looks like more of these symbols:

```
����q�J��˗�##Т���,�@��N���k��+��)Ȏy�̰s��2�%E!�ۏ=MT�q.���7���S�dy�F�֝N�������5����*�΁�X�_)������f�|���#�~b�~
```

The **Response Body** appears as seemingly **garbled**/**binary data**. These symbols **are not actual text from the website**. They indicate that **encoded** or **compressed response data** is being **interpreted as text** by **JMeter**. However, the **web browser handles the response correctly**, and both the **webpage** and its **source code** are **displayed as expected**.

**7** out of **8** **HTTP Requests** in my script have **encoded** or **compressed response data** within their **Response Bodies**, which means I am currently unable to **extract** **XSRF tokens** or use **Response Assertions** to verify that the script is working. I want to find out what **content encoding** the **responses** are using, so I open **View Results Tree**, select the **HTTP Request** that **loads the first page**, and select **Response headers** under the **Response data** tab. 

> **Content encoding** specifies how the **content** of an **HTTP response** is **encoded** or **compressed** for **transmission between the server and client**.

In the **Response headers**, I find these relevant lines:

- ```Content-Type: text/html; charset=UTF-8``` = specifies that the **response** contains **HTML content** and uses **UTF-8 character encoding**.
- ```Content-Encoding: zstd``` = specifies that the **response content** is **compressed** using **Zstandard** (**zstd**), a **data compression algorithm**, before being sent.

Therefore, I can conclude that there **is not** necessarily an **error** in this **response** or other **responses**, per se, but the **zstd content encoding** is **causing an issue** for this particular **JMeter script**. To get this **script** working correctly, I need to **configure** the **HTTP Requests** to **request a different content encoding**.

First, I will check which **content encodings** the **HTTP Request** that **loads the first page** accepts. I open **View Results Tree**, select the **HTTP Request**, and select **Request Headers** under the **Request** tab. There, I find the following relevant line:

```
Accept-Encoding: gzip, deflate, br, zstd
```

The next step is to **modify** the **HTTP Request headers** to **stop requesting** **zstd content encoding**. I will naturally start with the **HTTP Request** that **loads the first page**. **JMeter** has automatically created an **HTTP Header Manager** as a **child element** of each **HTTP Request**, and I open the first one.

Under the **Name:** column I find ```Accept-Encoding```, and under the corresponding **Value** column, I find ```gzip, deflate, br, zstd```. I **change** the **Value** to ```identity```. ```identity``` is the **HTTP content-coding value** that indicates **no content encoding should be applied**. In other words, I am **telling the server** to **send the response without compression**.

Now I run the script again, and the first **HTTP Request** successfully returns **readable source code**. The **1st Response Assertion** also works now, because the **text it is looking for** can be **found** in the **source code**:

```
<div class="hero">
    <h1>Test Authentication. Break Assumptions.</h1>
    <p>
        A simple playground for developers and security engineers to test login automation,
        authentication flows, and real-world edge cases.
    </p>
</div>
```

The next logical step is to **apply the same change** to all the other **HTTP Header Managers**: change the **Value** of ```Accept-Encoding``` to ```identity```. After that, most of the **HTTP Requests** execute **successfully** when I run the script. However, the **Response Assertions** for all the **font requests** (from **servers** ```fonts.googleapis.com``` and ```fonts.gstatic.com```) inside the **1st Transaction Controller** are failing. In **View Results Tree**, the **Assertion results** of the **Response Assertions** look like this:

```
Assertion error:false
Assertion failure:true
Assertion failure message:Test failed: text expected to contain /A simple playground for developers and security engineers/
```

This is expected, because these **font requests** do not contain the **text** the **Response Assertion is looking for**. This is due to **my previous mistake** of placing the **Response Assertion** under the entire **Transaction Controller**, instead of under the specific **HTTP Request**.

> It is good practice to place **Response Assertions** under **Samplers**, such as **HTTP Requests**, instead of under **Transaction Controllers**, which can contain multiple **Samplers**.

I place all **4 Response Assertions** under their respective **HTTP Requests**, and run the script once again. This time, **only** the **3rd Transaction Controller** fails. This is **expected** because I have not yet **correlated the XSRF token**.

I inspect the specific **HTTP Request** that fails the **Response Assertion**. It is the only **POST request** in my **test script**, whereas all the other **HTTP Requests** are **GET requests**.

- **GET request** = **asks** a **server** to **retrieve data** or a **resource**, such as an **HTML page**.
- **POST request** = **sends data** to a **server** for **processing**, such as **login credentials** or **form data**.

In the **Parameters** tab of this **POST request**, I see **3 items**:

1. ```email``` with **Value** ```xsrf@${host}```
2. ```password``` with **Value**  ```pa$$w0rd```
3. ```xsrfToken``` with **Value** ```ab6e97f5f559f233e171d07ed8377820```

> In the context of **computer programming**, a **parameter** is a **name-value pair** that **provides data** to an **HTTP request**, such as a **username**, **password**, or **XSRF token**.

I entered the **values** ```xsrf@authenticationtest.com``` (```email```) and ```pa$$w0rd``` (```password```) when **logging in** during **recording the script**, so they are **static** and should work as is. The reason why ```xsrf@authenticationtest.com``` has automatically been changed to ```xsrf@${host}``` is because ```authenticationtest.com``` was already **parameterized** using the **variable** ```host``` when the **Recording** template of this **Test Plan** was created. This can be seen in the **element** called **User Defined Variables**. In **JMeter**, ```${example}``` is the **syntax** for **variable substitution**, so therefore ```xsrf@${host}``` = ```xsrf@authenticationtest.com```.

```ab6e97f5f559f233e171d07ed8377820``` (```xsrfToken```), on the other hand, is a **dynamic value**, so it **will not work as is**. I need to **correlate** it. In order to do this, I first need to find the specific **HTTP Request** and the location in its **Response Body** where the **XSRF token** can be found and **extracted**. I find the easiest way is to first **run the script** and then use the **Search** function in **View Results Tree** to find the earliest **HTTP request** that contains the **keyword**. Since the **dynamic value** in my script is called ```xsrfToken```, I can use this as the **keyword**.

Using **Search** with the ```xsrfToken``` **keyword** in **View Results Tree**, I find a **match** in the **Response Body** of the only **HTTP Request** in the **2nd Transaction Controller**. Furthermore, using the **Find** function with the same **keyword** within the **Response Body** of this **HTTP Request**, I locate the **exact position** where the **XSRF token** can be **extracted**:

```
<input type="text" class="form-control" name="xsrfToken" id="xsrfToken" value="5b7096e07cab2173be59952324b7c64b"/>
```

After this, I create a **Regular Expression Extractor** under this **HTTP Request**. It can be done by **right-clicking** the **HTTP Request** (or other **Sampler**), hovering over **Add**, hovering over **Post Processors**, and selecting **Regular Expression Extractor**. In the **Regular Expression Extractor**, there are **4 settings** I am concerned with:

- **Name of created variable:** = what **JMeter** will call the **extracted value**. This **name** can then be used to **reference the extracted value** elsewhere in the **test script** using the ```${example}``` **syntax**.
- **Regular Expression:** = a **special text string** used to **describe a search pattern** that **JMeter** searches for.
- **Template (`$i$` where i is capturing group number, starts at 1):** = tells **JMeter** which part of the **regular expression match** to use as the **extracted value**. The **capturing groups** are the parts of the **regular expression** enclosed in **parentheses** = **()**. For example, ```$1$``` tells **JMeter** to use the **contents of the first capturing group**. In practice, this only matters if there are **multiple capturing groups** within a **regular expression**. If there is only **one capturing group**, then ```$1$``` should be used.
- **Match No. (0 for Random):** = which **matching occurrence** **JMeter** should **extract**. For example, ```1``` selects the **first match**, while ```2``` selects the **second match**. This matters if your **regular expression** finds **multiple matches in the same response**.

At this point, I am going to create the **regular expression** that will **extract** the **XSRF token**. There is a handy **website** for practicing **regular expressions**: https://regex101.com/. However, remember **not to paste** any **sensitive source code** there, as it is a **public website**. In my case, I can use it to create this **regular expression**, because the **source code** is already **publicly available**. I will use the following **string** as the **base**, since it is **unique** enough:

```
id="xsrfToken" value="5b7096e07cab2173be59952324b7c64b"/>
```

The completed **regular expression** looks like this:

```
id="xsrfToken"\s+value="([^"]+)"
```

I replaced the **literal space** with ```\s+```, replaced the **old XSRF token value** with ```([^"]+)```, and removed ```/>``` because it is not needed.

- ```\s+``` = matches **one** or **more** **whitespace characters**, such as **spaces** or **tabs**.
- ```([^"]+)``` = captures **one** or **more characters** that are **not quotation marks** as a **capturing group**. ```()``` create a **capturing group**, ```[^"]``` matches any character **except** ```"```, and ```+``` matches **one** or **more of those characters**.

If this **regular expression** works, it should **match the relevant text** and **extract only** the **value** of the **XSRF token**. For example, ```5b7096e07cab2173be59952324b7c64b``` will be **extracted** from the **string** ```id="xsrfToken" value="5b7096e07cab2173be59952324b7c64b"/>```.

Before adding this **regular expression** to the previously created **Regular Expression Extractor**, I can **test it beforehand** by using the **Search** and **Find** functions with the **Regular exp. option enabled** in **View Results Tree**. The **regular expression** can indeed find the **string I am looking for**, but there is one **caveat** with the **Find** function in **View Results Tree**: it **does not highlight** the **capture group**, which is the **part of the match that will be extracted**. But, I am quite certain this **regular expression** will work in practice.

I open the **Regular Expression Extractor**, and enter the following **values**:

- **Name of created variable:** = ```XSRF```
- **Regular Expression:** = ```id="xsrfToken"\s+value="([^"]+)"```
- **Template (`$i$` where i is capturing group number, starts at 1):** = ```$1$```
- **Match No. (0 for Random):** = ```1```

Finally, I change the **Value** of ```xsrfToken``` from  ```ab6e97f5f559f233e171d07ed8377820``` to ```${XSRF}``` in the previously discussed **POST request** under the **3rd Transaction Controller**.

Now when I **run the script** multiple times, it appears to be successful every time, and the **Response Assertions** are not failing. I can verify this further by comparing the **XSRF token value** of the **HTTP request** from which it is **extracted** to the **XSRF token value** in the **Request Body** of the **POST request**.

The **Response Body** of the **HTTP request** from which the **XSRF token value** is **extracted**:

```
<input type="text" class="form-control" name="xsrfToken" id="xsrfToken" value="c1894077910df231ee08323fd75faa3d"/>
```

The **Request Body** of the **POST request** where the **login credentials** and **XSRF token** are **submitted to the server**:

```
POST https://authenticationtest.com//login/?mode=xsrfChallenge

POST data:
email=xsrf%40authenticationtest.com&password=pa%24%24w0rd&xsrfToken=c1894077910df231ee08323fd75faa3d
```

The **XSRF token** (```c1894077910df231ee08323fd75faa3d``` **in this iteration**) is **identical in both requests**.

I can also **inspect** the **Response Body** of the **GET request** sent in response to my **POST request** in **View Results Tree**. As can be seen, the following **source code** provides **definitive confirmation of success**:

```
<h1>Login Success</h1>
<div class="alert alert-success">
	<strong>Success!</strong> You are now logged in!<br><br>

	You will be logged in for the next 10 minutes.
			If you wish to log out sooner, there is a Sign Out option in the top right corner.
	
	<br><br>
	For HTTP/NTLM Auth: Due to how browsers maintain this session, you may need to clear your browser cache to log out. There is no functional way for this site to provide a logout for this method. Something to think about if you plan on using this method.
</div>
```

My **script** can now **handle the dynamic XSRF token automatically**, which concludes the objective of this chapter.

> Even if you are certain that your **script works**, it is good practice to **test it again the next day**, because sometimes **scripts can stop working unexpectedly due to factors such as expired cookies**, **changed session data**, or **changes to the application**.


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
