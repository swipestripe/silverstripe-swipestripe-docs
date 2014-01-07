# Forms

Adding a product to the cart, updating the cart and processing an order are all areas that often require customization for ecommerce builds. Each of these three areas are managed by corresponding form classes:

- ProductForm
- CartForm
- OrderForm

Because the classes include all of the form fields and corresponding actions it is fairly straight forward to completely replace each area of functionality using ```Object::use_custom_class()```.

For instance, rather than using the ```updateFields()``` hook in OrderForm to alter the order form fields you can create an entirely new MyOrderForm class that replaces the original OrderForm class and override which fields are created and how different actions operate.

Alternatively there are numerous hooks throughout the form classes for extending the functionality of the forms without completely replacing the class.