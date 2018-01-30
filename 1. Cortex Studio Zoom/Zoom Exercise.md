# Zoom Exercise

###Start the appropiate web apps for Cortex:###
* For this exercise, the`Search` and `Cortex` webapps should already be running.

* If the `Search` and `Cortex` webapps are not running, you will need to launch them. Instructions on how to launch these web apps can be found in the `Maven` exercise in the `Exercise` folder found on the Desktop.

###Open Cortex Studio:###
* Open Google Chrome and either choose the `Studio` bookmark or browse to `http://localhost:9080/studio/`

* Authenticate as a `PUBLIC` user under the scope `mobee`

_Reminder: the scope is the store you are authenticing against_

###Enter the Shopper Details:###
* Navigate to the `Shopper's Default Profile` under `Entry Points`. After entering each resources required information, return to the `Shopper's Default Profile` to continue entering the next resources required information. The following details will need to be entered:
   * Address
      * Click the href link under `rel: "addresses"`
      * Click the href link under `rel: "addressform"` 
      * Enter the following address _(this will impact the tax applied to your order)_

      ```json
      address: {
        country-name: "US", 
        extended-address: "123", 
        locality: "WA", 
        postal-code: "20001", 
        region: "WA", 
        street-address: "123 Fake St"
      },
      name: {
            family-name: "Smith", 
            given-name: "John"
         },
      ```
      * Click the `createaddressaction` button to save the address
   * Email:
      * Click the href link under `rel: "emails"`
      * Click the href link under `rel: "emailform"` 
      * Enter any email and click the `createemailaction` button to save the email

###Add two different items to your cart:###
* Use the `Lookups` link under `Entry Points`

* Click on the href link under `rel: "itemlookupform"`

* Add the first item by typing the code `alien_sku` into the code text-field and click on the 
`itemlookupaction` button

* Click the href link under `rel: "addtocartform`

* Add a quantity of `1` for this item to your cart, then click the `addtodefaultcartaction` button

* Next add the second item to your cart by using the code `tt64464fn_hd` - again enter a quantity of `1`

###Verify you have two items added:###
* Navigate to `Shopper's Default Cart`

* Minimize the `self` and `links` open parenthesis. The response will be the following:

![](C:\Users\ep-trainee\Documents\Exercise_Images\zoom-mini.JPG)

_**Note:** This is a JSON response. Looking at structure of the response there are three things that are repeated in each request: a self object, one or more messages and links._

# Construct a Zoom to build the below page
![](C:\Users\ep-trainee\Documents\Exercise_Images\Example_Cart.PNG)
* Navigate back to the `Shopper's Default Cart`. 

	_How can you tell you're in the cart resource?_

**Part 1:**
* Create a Zoom to return the name of each item in the cart

**Part 2**
* Append the prices of each item in the cart to the Zoom _(should include both the `list-price` and the `purchase-price`)_

	_Hint: Search on the item level to find the items prices_

**Part 3:**
* Append the Cart Total to the Zoom

**Part 4:**
* Append the Order Total to the Zoom

_What is the difference between the Cart and Order totals?_

**Part 5:**
* Append the Tax applied to the sale to the Zoom

###Enter the following missing information to expose the purchase button###

* Payment token:
	* Click on the href link under `rel: "paymenttokenform"`. Enter the following:
		* display-name: token123
		* token: 12345
	* Then click the `createpaymenttokenformorderaction` button
	
**Part 6:**
* Append the purchase button href link to the Zoom

_Hint: All `needinfo` identifiers need to be completed before you can view the `"submitorderaction"` button_
