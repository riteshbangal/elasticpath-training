#How to Zoom

###Start the appropiate web apps for Cortex:###
* Ensure no webapps are already running, then launch the `Search` and `Cortex` web apps.

_**Hint:** To close a web app use the command `Ctrl + c`. This ends the process gracefully - so no applications will be runnnig in the background._

_**Hint:** All the commands to launch web apps are in the `Maven` exercise in the `Exercise` folder found on the Desktop_

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
* Add the first item by typing the code `alien_sku` into the code text-field and click on the `itemlookupaction` button
* Click the href link under `rel: "addtocartform`
* Add a quantity of `1` for this item to your cart, then click the `addtodefaultcartaction` button
* Next add the second item to your cart by using the code `tt64464fn_hd` - again enter a quantity of `1`

###Verify you have two items added:###
* Navigate to `Shopper's Default Cart`
* Minimize the `self` and `links` open parenthesis. The response will be the following:

![](C:\Users\ep-trainee\Documents\Exercise_Images\zoom-mini.JPG)

_**Note:** This is a JSON response. Looking at structure of the response there are three things that are repeated in each request: a self object, one or more messages and links._

## Example 1: Display the items name as part of the returned JSON response##
**Part 1: Finding the location of the items name:**
* In `Shopper's Default Cart` open the `link` parenthesis
* Follow the href link for the `lineitems`
* Follow the href link for the `element`
* Follow the href link for the `item`
* Follow the href link for the `definition`
* Minimize the `self`, `details` and `links` open parenthesis. The response should be the following:

![](C:\Users\ep-trainee\Documents\Exercise_Images\alien.JPG)

_Note: This display-name portion is what you want to return as part of the Zoom._

**Part 2: Creating the Zoom**
* Navigate back to the `Shopper's Default Cart`
* In the Zoom text-field enter the following: `lineitems:element:item:definition` and click the `Submit` button 

_Note: The Zoom is following the path of `href` links to get the piece of information you require as you manually did above_

* Close the all the `self`, `links` and `details` parenthesis. The response should be the following:

![](C:\Users\ep-trainee\Documents\Exercise_Images\zoom-ex1.JPG)

Now in one JSON response we have returned the `total-quantity` of the order as well as the `display-names` for both of the items in the cart.

##Example 2: Appending more than one Zoom##
To append two (or more) Zooms together use a comma `,` between the Zoom Calls

**Example Obecjtive:**
* Return the SKU code and the name of an item

**Steps:**
* Navigate to `Lookups` and search for the DVD Alien using the code `alien_sku`
* From looking at the Request URI as well as the first `self` tag's `type` property, you can tell the location is the `item` resource
* Enter the following into the Zoom text-field: `code,definition` and click the `Submit` button. 
* Minimize the `self`, `links` and `details` tags, the JSON response will be the following:

![](C:\Users\ep-trainee\Documents\Exercise_Images\zoom-ex2.JPG)