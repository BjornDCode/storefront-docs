# Installation
- [Shopify Store](#shopify-store)
    - [Sample Data](#sample-data)
    - [Making products available for the API](#available-for-api)
- [Installation](#installation)
- [Configuration](#configuration)

<a name="shopify-store"></a>
## Shopify Store
Before downloading Storefront, make sure you have a Shopify Store set up. If you don't have a Shopify subscription you can create a free [developer store](/docs/{{version}}/shopify#developer-account).

Next you need a Storefront Access Token. This is created though a private app in the Shopify backend. Follow this [link](https://help.shopify.com/api/storefront-api/getting-started#authentication) to see how you can create an Access Token. I recommend to call your private app 'API'.

<a name="sample-data"></a>
### Sample Data
If you don't yet have product data for your shop there is a few ways to generate sample data. 

The easiest way to get started is by downloading the [Simple Sample Data](https://apps.shopify.com/simple-sample-data) app. Simply install it, and generate the data you want.

If you prefer another dataset you can [download](https://www.shopify.com/partners/blog/93467590-design-your-store-faster-with-product-csvs-and-images) and import sample datasets from some popular Shopify themes. 

<a name="available-for-api"></a>
### Making products available for the API
By default your products won't be available to be accessed through the API. If you go to 'Products' in the Shopify backend, you will see a message underneath each product saying it's 'unavailable in <private app>'.

#### Make a single product available
1. Click on 'Products'
2. Click on the product
3. Check off your private app
4. Click 'Done'

This is cumbersome to do for every single product, so instead you can buld edit your products.

#### Make all products available
1. Click on 'Products'
2. Click on 'Filter' > 'Availability' > 'Unavailable on <private app>'
3. Bulk select all products
4. Click on Actions' > 'Make products available' and select your private app

Now your Shopify Store is ready to use with Storefront. 
If you want to test the API before setting up Storefront you can follow [these steps](https://help.shopify.com/api/storefront-api/getting-started#accessing-the-storefront-api-graphql-endpoint).

<a name="installation"></a>
## Installation
Install

<a name="configuration"></a>
## Configuration
Configure