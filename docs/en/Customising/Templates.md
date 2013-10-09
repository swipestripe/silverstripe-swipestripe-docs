# Templates

SwipeStripe is shipped with all the templates you need to customise the look and feel of your shop in accordance with the design of your website.

The templates shipped with SwipeStripe will be used by default, however, you can copy/paste the template files into your own themes directory and overwrite them to change the look and feel easily.

Template files are used extensively for rendering pages, forms, form fields and emails - so it is often just a matter of overriding the template files to change the design of a certain component.

All the CSS that has been used in SwipeStripe uses the selector .sws - this selector appears at the top of many template files for this reason. To remove all the styles that SwipeStripe has applied to a template you can often just remove this selector.

SwipeStripe has used the [Bootstrap](http://getbootstrap.com) library to apply cross browser compliant styles to tables, forms etc. 

## Main Pages
The main client facing pages that are created for you when SwipeStripe is installed are:

Cart  
Checkout  
Account

There are also Product pages which you will create yourself.

Templates for all of these pages are in swipestripe/templates/Layout/

### AccountPage.ss
This is the main account page with links to a customers orders. This is also the destination page when a customer logs in to the website. You can add content here for customer greetings etc.

### AccountPage_order.ss
This is for the order() action on AccountPage.php, to display an order to a customer. This template uses a lot of Includes/ to render the order.

### CartPage.ss
For displaying the cart, this template is really just a holder for $CartForm which uses Includes/CartForm.ss to render.

### CheckoutPage.ss
The checkout page is also really just a holder for OrderForm.ss which uses Includes/OrderForm.ss to render.

### Product.ss
The product page includes the product details, the first image for the product, the product price and a form for adding a product to the cart. 

If you just want to use SwipeStripe as a catalogue in the short term and perhaps add full ecommerce capabilities to your site at a later stage you can easily edit this template to remove the $ProductForm.

If you want to redirect a customer to another page (such as a checkout) immediately after they have added a product to their cart you can pass a second argument to $ProductForm which will redirect the customers browser.

One thing to note, the product page displays the price like so:

:::xml
	<h3 class="product-price-js">$Product.Price.Nice</h3>
	
If your product has variations and one variation has an amount it increases the product price by, this price value will be updated from the javascript when the options for that variation are chosen by a customer.

So it is important to keep the class "product-price-js" so that the javascript can find the price value to update if necessary. 


