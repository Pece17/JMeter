# JMeter

**JMeter** instructions.


## Recording Test Scripts

1. open **apache-jmeter-5.6.3** folder -> **bin** -> **ApacheJMeter.jar**
2. write **Test Plan** to **Name:**
3. click **File** -> **Save Test Plan as** -> **Save In:** to **C:\JMeter-skriptit** -> write **Test Plan.jmx** to **File Name:** -> **Files of Type:** as **All Files** -> **Save**
4. click **File** -> **Templates...** -> select **Recording** -> **Create**
5. **hostToRecord:** as ```www.saucedemo.com``` -> **Create**
6. select **HTTP(S) Test Script Recorder** -> **▶ Start** -> **Stop**
7. open **Google Chrome** -> **Search box** -> ```chrome://certificate-manager/``` -> **Installed by you** -> **Trusted Certificates** -> **Import** -> find **ApacheJMeterTemporaryRootCA.crt** from ```\apache-jmeter-5.6.3\bin``` -> **Open**
8. **HTTP(S) Test Script Recorder** -> **▶ Start** https://www.saucedemo.com/ -> **Transaction name** as ```1``` for the first page
