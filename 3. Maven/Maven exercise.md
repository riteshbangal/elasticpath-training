# Starting EP web applications

##Start the fake SMTP server:##

* Open a windows explorer, navigate to `C:\Tools` directory
* Double click `fakeSMTP-2.0.jar` to launch the application
* Click the `Start Server` button

##Start the JMS / ActiveMQ Server:##

* Open a windows command prompt
* Rename the window using the following command:

![](C:\Users\ep-trainee\Documents\Exercise_Images\JMS.JPG)

##Start the Search Server:##

_**Hint:** Have you already started the Search Server? There should only be one instance of each server running at a time. If you have the Search Server already running, please gracefully close the instance using the command `crtl+c`._

* Open another windows command prompt
* Rename the window using the following command:

![](C:\Users\ep-trainee\Documents\Exercise_Images\search.JPG)

_**Pop Quiz:** Why was the `clean` part of the Maven commend left out when starting up the Search Server?_

##Start the CM Administration server:##

* Open another windows command prompt
* Rename the window using the following command:

![](C:\Users\ep-trainee\Documents\Exercise_Images\cm.JPG)

##Configuration Change in Commerce Manager Administration Console - _Pointing the mail host to localhost_

* Open the browser and navigate to the `CM Administration` link found on the bookmarks bar.
* Password for the admin user is `111111`
* click  `Configuration` gear icon in the middle of the top navigation bar. Or press `Alt-9`
* On the left hand panel, under `System Administration`, click on `System Configuration`
* In the main window on the right hand side, use the Filter Option so search for `mailHost`
* Click on the Setting Name `mailHost` and use the Edit button next to Filter and change the default value from `YOUR_STMP_HOST` to `localhost`

_**NB:** It is important to wait until this system setting is changed before starting up the `Cortex` Server_

##Start the Cortex Server:##

* The following web application needs to be running to use Cortex Studio
* Open another windows command prompt
* Rename the window using the following command:

![](C:\Users\ep-trainee\Documents\Exercise_Images\cortex.JPG)

##Start the Integration Server:##

_If the Integration server is not running, the message created by the JMS server will not get processed_

* Open another windows command prompt
* Rename the window using the following command:

![](C:\Users\ep-trainee\Documents\Exercise_Images\int.JPG)

##Complete an Order in Cortex Studio:##

###Opening Cortex Studio###
_Both the **Search** Server nad **Cortex** Server must be running to use Cortex Studio_
* Open Google Chrome and choose the `EP Studio` bookmark or browse to `http://localhost:9080/studio`
* Open up `Authentication` which can be found on the right hand panel. Ensure the scope is `mobee` _(this refers to a catalog in CommerceManager)_ and authenticate as a `PUBLIC` user

###Add an item to the Shopper's Cart###
* Under `Entry Points` click `Searches`
* Click on the href link under the `keywordsearchform`
* Search for `alien` in the Keywords textbox and click the `itemkeywordsearchaction` button
* Click on the href link under the `rel: "element"`
* Click on the href link under `rel: "addtocartform"`
* Change the quantity from 0 to 1 in the quantity textbox, then click the `addtodefaultcartaction` button

###Navigate to the Shopper's Current Order###
* Under `Entry Points` click the `Shopper's Current Order`

_Orders may have flashing `NeedInfo`s. `Needinfo`s identify a condition that must be satisfied before a transaction can complete. `Needinfo`s link to a selector or form where the customer can select or enter the missing condition. Once the `Needinfo`s are satisfied the order can be submitted to a purchase._

###Enter in missing information to complete purchase###
The following `Needinfo`s require additional information. Once you have entered the required information, to return to the `Shoppers Current Order` click the `Shopper's Current Order` link found under `Entry Points` and scroll down until you hit the next flashing `Needinfo` and click on the href link beneath it
* Default Shoppers email:
	* Click on the href link under the `rel: "emailform"`. 
		* Provide the following email address: `email@email.com` 
		* Then click the `createemailaction` button
* Shoppers Address:
	* Click on the href link under the `rel: "addressform"`. Complete the address as follows:
		* country-name: `US`
		* extended-address: `test`
		* locality: `WA`
		* postal-code: `20001`
		* region: `WA`
		* street-address: `123 Fake Street`
	* Enter any `family-name` and `given-name` 
	* Then click the `createaddressaction` button
* Payment token:
	* Click on the href link under `rel: "paymenttokenform"`. Enter the following:
		* display-name: token123
		* token: 12345
	* Then click the `createpaymenttokenformorderaction` button
	
###Submitting the Shopper's Order###
* To complete the purchase stay within the the `Shopper's Current Order` and click the href link under `rel: "purchaseform"`
* Then click the `submitorderaction` button. You should be redirected to the newly created purchase

_If there are any flashing `NeedInfo`s at this time the `submitorderaction` button will be hidden. You will need to review the aboves steps and enter any missing information_

###Validation:###

On successful submission of the order, Cortex kicks off an order creation event which is added to the ActiveMQ queue and handled by the integration server. The integration server will send the order confirmation event which you can now view in the `Fake SMTP server`.

##Logging##

**Note:** The log files for the web applications you started can be found in the following location: [`C:\Users\ep-trainee\ep\logs`](\C:\Users\ep-trainee\ep\logs).

Elastic Path Commerce uses two logging frameworks for recording activities during run time. Cortex uses [Logback](https://logback.qos.ch/), while the rest of the core platform web applications use [Apache log4j](http://logging.apache.org/log4j/1.2/). Apache log4j is a configurable logging utility for Java that can output messages to a console and a log file. Cortex uses Logback as it incorporates the [SLF4J (Simple Logging Facade for Java) API](https://www.slf4j.org/), provides OSGi logging, and has JMX support. Logback can also output messages to a console and a log file. For more information please see our [Developers Guide](https://developers.elasticpath.com/commerce/7.0/Core-Commerce-Development/Cross-Platform-Technologies/Logging).