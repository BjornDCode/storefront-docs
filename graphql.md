# GraphQL
[GraphQL](https://graphql.org/) is a modern way to query data. To work with GraphQL you need two things: A GraphQL server (which Shopify provide), and a client to query the API. 

> GraphQL is a query language for APIs and a runtime for fulfilling those queries with your existing data. GraphQL provides a complete and understandable description of the data in your API, gives clients the power to ask for exactly what they need and nothing more, makes it easier to evolve APIs over time, and enables powerful developer tools.

One of the main features of GraphQL is that you get exactly what you ask for. And no more. 

This is a sample request for Shopify:
```
{
    shop {
        name
        description
        primaryDomain {
            url
            host
        }
    }
}
```
The response you would get would be this:
```
{
    "data": {
        "shop": {
            "name": "My Shop Name",
            "description": "My Shop Description",
            "primaryDomain": {
                "url": "https://myshop.myshopify.com",
                "host": "myshop.myshopify.com"
            }
        }
    }
}
```
As you can see the request models the data that is returned. 

Another powerful feature of GraphQL is that you can get many resources in a single request. 

Let's take another example:
With a normal REST API it's common that you have to hit multiple endpoints to get all the data you need. Let's say you want some information about a shop, but also a list of products. You would hit a `/shop` endpoint to get information about the shop, and after that request is finished you would hit a `/products` endpoint to get the list of products. 

With GraphQL you can do it all in one query:
```
{
    shop {
        name
        description
        primaryDomain {
            url
            host
        }
        products(first: 20) {
            edges {
                node {
                    title
                    description
                    handle
                    variants
                }
            }
        }
    }
}
```
This is a way you can query for products in Shopify. Notice that we just expanded the request from earlier so we will just have to call this request once, to get all the data needed. 

There's a lot more to learn about GraphQL, but these are some of the core concepts to understand. If you want to learn more you can have a look [here](https://graphql.org/learn/).
