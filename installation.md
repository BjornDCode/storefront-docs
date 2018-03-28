# Installation
- [Shopify Store](#shopify-store)
    - [Sample Data](#sample-data)
    - [Making products available for the API](#available-for-api)
- [Installation](#installation)
- [Configuration](#configuration)
    - [Options](#options)

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
You can install Storefront through NPM, alongside your other dependencies. The library itself has some dependencies that must be installed though:

- ```apollo-cache-inmemory```: A cache implementation for Apollo Client
- ```apollo-cache-persist```: A library to cache data in browsers
- ```apollo-client```: A library making it easy to work with GraphQL servers. See more [here](/docs/{{version}}/apollo).
- ```apollo-link```: A network interface for Apollo Client.
- ```apollo-link-http```: An HTTP implementation of ```apollo-link```
- ```graphql```: A Javascript reference implementation of GraphQL
- ```graphql-tag```: A set of utilities to make GraphQL queries
- ```siema```: A small Javascript slider that is used in the Product Image components
- ```vue-apollo```: A Vue implementation of Apollo Client
- ```vue```: A Javascript framework which Storefront is built upon.

Most of these dependencies you don't have to worry about. Read the [prerequisites](/docs/{{version}}/vue) for the things that are recommended to know in order to work with Storefront.

```
npm install --save vue-storefront apollo-cache-inmemory apollo-cache-persist apollo-client apollo-link apollo-link-http graphql graphql-tag siema vue-apollo vue
```

<a name="configuration"></a>
## Configuration
After installing Storefront and it's dependencies you can start configuring it. Create an index.js file that looks like this:

```
import Vue from 'vue';
import Storefront from 'vue-storefront';
import { InMemoryCache } from 'apollo-cache-inmemory';
import { persistCache } from 'apollo-cache-persist';
import App from './App';

const cache = new InMemoryCache();

// Specify where you want the cache saved. Click here for a full list of options: https://github.com/apollographql/apollo-cache-persist#storage-providers
const persistor = persistCache({ cache, storage: window.sessionStorage, debug: true, debounce: 0 });

// You have to pass your store details, as well as the cache and persistor objects to Storefront. See all possible options below.
const options = {
    domain: 'https://vue-protoype.myshopify.com',
    storefrontAccessToken: 'c3513ad829bbdffaff24e80f9228db62',
    cache,
    persistor
}

// Instantiate Storefront
Vue.use(Storefront, options);

// Persistor restores data from the cache. This is an async operation. Therefore we have to wait for the data to be restored before initialising Vue.
persistor.then(() => {
    new Vue({
        el: '#app',
        provide: Vue.provider(),
        render: h => h(App)
    })
})
```
Link ```index.js``` in your index.html file and you are ready.

<a name="option"></a>
### Options
When initialising Storefront, you must pass it an object of options.

Here is a list of required and possible options:

```domain``` (required)
Domain is your Shopify store domain. It must be an absolute path like this: ```https://storefront-demo.myshopify.com```

```storefrontAccessToken``` (required)
The access token generated by your private app. If you don't yet have an access token click [here](#shopify-store).

```cache``` (required)
An instance of ```InMemoryCache``` from ```apollo-cache-inmemory```

```persistor``` (required)
An instance of ```persistCache``` from ```apollo-cache-persist```

```router``` (optional)
You can pass an instance of ```vue-router``` to automatically register routes. Click [here](/docs/{{version}}/views) for a list of routes that are registered.
