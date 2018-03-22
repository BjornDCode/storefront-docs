# Introduction
- [Introduction](#introduction)
- [Issues](#issues)
  - [Themekit](#themekit)
  - [Liquid](#liquid)
  - [Rigid Structure](#rigid)
  - [Compiling Javascript](#compilejs)
  - [SASS](#sass)
  - [Modern Frameworks](#modernframeworks)
- [An alternative way](#alternativeway)
- [License](#license)
- [Demo](#demo)

<a name="introduction"></a>
##Introduction
Storefront is a Javascript library for making front ends for Shopify websites. [Shopify](https://www.shopify.com/) is a great tool to manage and run your webshop. The traditional way of building a Shopify website is by creating a theme. But when creating Shopify themes there are some downsides. Storefront aims to overcome these issues and create a smooth developer experience while still producing great end results.

If you are building a commercial project you need to [buy a license](#license).

<a name="issues"></a>
## Issues with Shopify development

<a name="themekti"></a>
### Themekit
You have to maintain a connection between your local development environment and Shopify. This is done using [Themekit](https://shopify.github.io/themekit/). Everytime you make changes to your theme, Themekit will upload the changes. This process can take a few seconds. This is enough to break your flow and can create a frustrating developer experience.

<a name="liquid"></a>
### Liquid
You are also forced to use [Liquid](https://help.shopify.com/themes/liquid), a templating language made by Shopify. Liquid is a decent templating language, but you still have to learn new syntax, new caveats and other overheads that comes with learning a new language. Documentation and code examples for Liquid is also lacking quality.

<a name="rigid"></a>
### Rigid Structure
Shopify websites are server-side rendered. That means you are locked into using Shopify's URL structure. If you want to create a page showing all products from a specific vendor you have to create a collection containing the products and show that  collections's page. This can result in messy URL's like domain.com/collections/paul-smith. It's not immediately clear that it's a vendor specific page. 

<a name="compilejs"></a>
### Compiling Javascript
Compiling Javascript from ES6 to ES5 can be tricky. You need to setup a build process that's running separately from Themekit. This limits the available tools you have access to from NPM

<a name="sass"></a>
### SASS
Shopify compiles SASS on the server. But the version of SASS used is usually several version behind the most current version. This is to protect websites from breaking changes in newer versions of SASS. But it also limits you from using the latest features.

<a name="modernframeworks"></a>
### Modern Frameworks
Working with a modern Javascript framework such as React, Vue or Angular is either impossible or tricky to set up. Building a  Single Page Application is not possible.

All these issues can create a less than ideal experience. 

<a name="alternativeway"></a>
## An alternative way to build Shopify stores
Storefront was built to solve these issues and create a great developer experience. It's a Javascript library built on top of Vue. Data is fetched from the [Storefront API](https://help.shopify.com/api/storefront-api) using [Apollo Client](https://www.apollographql.com/client/). 

Storefront decouples the backend from the front end. You will still handle everything in the Shopify backend. The front end is build separately and can be hosted anywhere. 

Apollo handles all contact with the Shopify API. It automatically handles errors, loading states and caching of content. 

The Storefront API is a [GraphQL](https://graphql.org/) API. This makes it possible to only grab the data that is absolutely needed, resulting in smaller queries. You don't need to know much about GraqhQL to use Storefront. 

Storefront also comes with pre-built components. This components can be modified as needed by you or plugged straight into your project.

<a name="license"></a>
## License
When you are launching your Storefront project you need to buy a license. You can do that right [here](/#license). A license costs <b>49$</b> and is valid for one website or project.

You are free to use Storefront for open source projects. That means you are free to download the library if you want to play around with it or build a demo to show your clients. 

If you have any questions regarding licensing feel free to [contact me](/support).

<a name="demo"></a>
## Demo
Click [here](#) to see a demo store built with Storefront.
