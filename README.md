# JMeter

**JMeter** instructions.


## Recording Test Scripts

1. open **apache-jmeter-5.6.3** folder -> **bin** -> **ApacheJMeter.jar**
2. write **Test Plan** to **Name:**
3. click **File** -> **Save Test Plan as** -> **Save In:** to **C:\JMeter-skriptit** -> write **Test Plan.jmx** to **File Name:** -> **Files of Type:** as **All Files** -> **Save**
4. click **File** -> **Templates...** -> select **Recording** -> **Create**
5. **hostToRecord:** as ```the-internet.herokuapp.com``` -> **Create**
6. select **HTTP(S) Test Script Recorder** -> **▶ Start** -> **Stop**
7. open **Google Chrome** -> **Search box** -> ```chrome://certificate-manager/``` -> **Installed by you** -> **Trusted Certificates** -> **Import** -> find **ApacheJMeterTemporaryRootCA.crt** from ```\apache-jmeter-5.6.3\bin``` -> **Open**
8. while in **Google Chrome** **Settings** -> **System** -> **Open your computer's proxy settings** -> **Manual proxy setup** -> **Set up** -> change **Use a proxy server** as **On**, **Proxy IP address** as ```127.0.0.1```, and **Port** as ```8888``` -> **Save**
9. **HTTP(S) Test Script Recorder** -> **▶ Start** https://the-internet.herokuapp.com/ -> **Transaction name** as ```1``` for the first page
