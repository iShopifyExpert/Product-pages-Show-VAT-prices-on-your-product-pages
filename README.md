If your government requires you to show prices with taxes included, but you want your international customers to pay less than the VAT-included price, you will need to show two prices in your shop. One price will be with taxes included for your local customers, and one price will be without taxes for your international customers.


Tip: The solution presented here won't work in the following themes: Venture and Boundless.


Note: This solution will only work if your products have only one variant, and the price on the product page is not updated via JavaScript (usually found in a selectCallback function).


 

Set your tax rates
 

 

Shopify will automatically set your tax rates for you, but you might want to confirm that those rates are correct. To do so:

 

From your Shopify admin, go to Settings > Taxes.
Look at the tax rates. Click on the country's name to change a country's tax rate.
In the Tax Calculations section, make sure that the Show all prices with tax included checkbox is unchecked.

vat-01.png

Save any changes.
 

Edit your theme
 

 

We're going to find the locations where the theme calls on product price. This will generally appear as:

 

{{ product.price | money }}
 

We will want to add in a variable here that will multiply the price by your tax rate:

 

{{ product.price | times:1.XX | money }}
 

Where XX = your tax rate. So if your tax rate is 10%, it should be times:1.1. If it's 5%, it should be times:1.05. In Canada, the federal tax rate is 5%, so we'll use times:1.05.

 

This tutorial will use the Minimal theme as an example — every theme is built differently, so the areas where you have to modify your theme will differ if you're using another theme.

 

From your Shopify admin, go to Online Store > Themes.
Find the theme you want to edit, and then click Actions > Edit code.
There are four main places where we'll want to change the code to affect how prices are displayed:

the product page
the collection page
the homepage
the cart page
 

Home Page and Collection listings
 

 

The Minimal theme changes this in the exact same spot.


From your Shopify admin, go to Online Store > Themes.
Find the theme you want to edit, and then click Actions > Edit code.
Click the Snippets folder to expand and view the folder's contents.
Click the product-grid-item.liquid snippet to open it in the online code editor.
Locate the following: 

{{ product.price | money }}
 

Change it to:

{{ product.price | times:1.05 | money }} Int price: {{ product.price | money }}
So that it looks like this:

vat-02.jpg

Save your changes.
 

Product page
 

 

Under the Templates folder, locate and click on product.liquid to open it in the online code editor.
In the online code editor, look for:

{{ product.price | money }}
 

Change that to:

{{ product.price | times:1.05 | money }}
 

Under <div class="purchase">, add:

<h3>Int price: {{ product.price | money }}</h3>
before the closing </div> tag.

It should look like this:

vat-03.jpg

Save your changes.
 

Cart
 

 

Showing the international price for each line item in the table will most likely just make the page very cluttered and confusing. So we'll just add a note at the top of the page that lets international customers know that they will receive 5% off of the listed price. We will also add an international price at the end of the cart.

 

Under the Templates folder, locate and click on cart.liquid to open it in the online code editor.
Under the opening <div>, add:

<h3 style="text-align:center; color:red">All international orders receive 5% off!</h3>
So that it appears like this:

vat-04.jpg

We'll now change the line item prices in the table so that they are also marked up:


{{ item.line_price | money }}

Changes to:


{{ item.line_price | times:1.05 | money }}

So that it appears as such:

vat-05.jpg

We'll now add the international final price below the regular final price. Change:

{{ cart.total_price | money }}
to

{{ cart.total_price | times:1.05 | money }} <br /> Int price: {{ cart.total_price | money }}
Save your changes.
Your shop will now show both your prices including VAT as well as your international price without. Check out this test shop to see how it works.
