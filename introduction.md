# Introduction

Storefront is a Javascript library for making front ends for Shopify websites. [Shopify](#) is a great tool to manage and run your webshop. The traditional way of building a Shopify website is by creating a theme. But when creating Shopify themes there are some downsides. Storefront aims to overcome these issues and create a smooth developer experience while still producing great end results. 

## Issues with Shopify development

*   You have to maintain a connection between your local development environment and Shopify. This is done using [Themekit](#). Everytime you make changes to your theme, Themekit will upload the changes. This process can take a few seconds. This is enough to break your flow and can create a frustrating developer experience.
*   You are also forced to use [Liquid](#), a templating language made by Shopify. Liquid is a decent templating language, but you still have to learn new syntax, new caveats and other overheads that comes with learning a new language. Documentation and code examples for Liquid is also lacking quality.
*   Shopify websites are server-side rendered. That means you are locked into using Shopify's URL structure. If you want to create a page showing all products from a specific vendor you have to create a collection containing the products and show that  collections's page. This can result in messy URL's like domain.com/collections/paul-smith. It's not immediately clear that it's a vendor specific page. 
*   Compiling Javascript from ES6 to ES5 can be tricky. You need to setup a build process that's running separately from Themekit. This limits the available tools you have access to from NPM
*   Shopify compiles SASS on the server. But the version of SASS used is usually several version behind the most current version. This is to protect websites from breaking changes in newer versions of SASS. But it also limits you from using the latest features.
*   Working with a modern Javascript framework such as React, Vue or Angular is either impossible or tricky to set up. Building a  Single Page Application is not possible.

All these issues can create a less than ideal experience. 

## An alternative way to build Shopify stores

Storefront was built to solve these issues and create a great developer experience. It's a Javascript library built on top of Vue. Data is fetched from the [Storefront API](#) using [Apollo Client](#). 

Storefront decouples the backend from the front end. You will still handle everything in the Shopify backend. The front end is build separately and can be hosted anywhere. 

Apollo handles all contact with the Shopify API. It automatically handles errors, loading states and caching of content. 

The [Storefront API](#) is a [GraphQl](#) API. This makes it possible to only grab the data that is absolutely needed, resulting in smaller queries. You don't need to know much about GraqhQl to use Storefront. 

Storefront also comes with pre-built components. This components can be modified as needed by you or plugged straight into your project.

## Demo