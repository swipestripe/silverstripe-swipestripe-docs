# Guest Checkout

To create a guest checkout simply remove the password fields from the checkout page order form. 

This could be achieved by replacing the OrderForm class altogether using Object::use\_custom\_class() or altering the OrderForm.ss template so that the PersonalDetailsFields are not included but are instead replaced with a single Email field.

When the order is generated an email address is still required in order to send email confirmations of the order, with this email address a Customer (type of Member) is created but if the password fields are ommitted then the customer's password will not exist.

After the order is completed (payment has completed) the customer is automatically logged in and redirected to the order summary page in their account. However, next time they visit the site after their session has timed out they will not be able to log in - they will still be able to follow the "Forgot password" procedure though.

In a way this is not a guest checkout as we still create an account for each customer in the background but it should suffice in most cases.