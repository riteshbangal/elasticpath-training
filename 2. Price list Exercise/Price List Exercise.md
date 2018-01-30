#Price List & Price List Assignment Exercise 

In this exercise we will be creating a new Price List with a designated currency, a single product, and that products price. Then you will create a Price List Assignment which will detail the suitable conditions for the Price List to trigger.

Before using the web **Admin Console**, the **CM SEVER** and **SEARCH SERVER** need to be running. For instructions on how to start these, please refer to _C:\Users\ep-trainee\Desktop\Exercises\1. Maven.md_

##Create a Price List

Open Google Chrome and click the **CM Administration** bookmark.

Enter the following details to login:

| Username | Password | 
| -------- |:--------:| 
| admin    | 111111   | 

To open the **Price List Manager**, click on the **$** symbol from the top navigation bar. _(Alternatively press Alt+2)_

From the top navigation, click the **$** symbol with the **+** symbol attached to it to create a new Price List.

Create a new Price List by entering the following informatoin in the **Price List Summary* tab. 

| Price List      | Description   | Currency  |
| --------------- |:-------------:| ---------:|
| A Test Price List | EUR pricing   | EUR       |

Once complete, click the **Save** icon. _If you do not click the Save icon, you will not be able to continue with the exericse._

Open the **Prices** Tab.

Click “Add Price…” and enter the following details

| Type     | Code      | Quantity  | List Price | Sale Price |
| -------- |:---------:| ---------:| ----------:| ----------:|
| SKU      | alien_sku | 1         | 15.99      | 5.99       |

Once complete, click the **Save** icon.

_**Hint:** To view other Price Lists, click the **Search** button in the left hand panel._

##Create a Price List Assignment

From the top navigation, click the **$** symbol with the **+** and **cog** symbol attached to it to create a new Price List Assignment.

###Step 1:
Enter the following information:

| Name                        | Description   | Priority  |
| --------------------------- |:-------------:| ---------:|
| A Europe Pricing All Custmers | EUR pricing   | 1         |

Throughout these steps, lick the **Next** button to continue.

###Step 2:
From the list of Price Lists, choose the Price List you created above.

_**Hint:** Use the filter to make the list smaller._

###Step 3:

Select the **Mobile Virtual Catalog**.

###Step 4:

Select **All Shoppers**.

###Step 5:

Select **All the time (effective immediatelly)**.

###Step 6:

Choose **All Stores** and click the **Finish** button.

##Verify your Price List and Price List Assignment##

###Step 1:
Open Cortex Studio by opening Google Chrome and either choose the `Studio` bookmark or browse to `http://localhost:9080/studio/`.
Authenticate as a `PUBLIC` user under the scope `mobee`

###Step 2:
Search for the product `Alien` by name, or using the product code `alien_sku` and open up the items Price resource.

###Step 3:
Under the Request Header section, enter the following under `X-Ep-User-Traits`:
```
CURRENCY=EUR
```

Prefrom a `GET` operation on the resource by clicking the `Submit` button. 

Validate that the `prices.item-price` has the following structure:

```
{
   self: {
      type: "elasticpath.prices.item-price", 
      uri: "/prices/items/mobee/<item-id>", 
      href: "http://localhost:9080/cortex/prices/items/mobee/<item-id>"
   }, 
   messages: [ ], 
   list-price: [
      {
         amount: 100, 
         currency: "EUR", 
         display: "€15.99"
      }
   ], 
   purchase-price: [
      {
         amount: 25, 
         currency: "EUR", 
         display: "€5.99"
      }
   ], 
   links: [ ]
}
```

##Commerce Manager / Administration Console User Guide##

For Help or for further instructions on how to use the CM Administration console please reference the **User Guide**.

This guide can be found by clicking the down arrow on the User Menu on the top right hand corner where the users name is displayed. _If you are currently logged in as "admin", it will display "admin"._

Then click the option "? Help". This will launch the User Guide.