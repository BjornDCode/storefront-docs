# Apollo
The Apollo Platform is a set of tools that can make working with GraphQL easier. Storefront uses [Apollo Client](https://www.apollographql.com/client) to fetch data from Shopify. Therefore it's a good idea to know the basics.

Apollo Client is a very powerful tool when fetching data from a GraphQL API. It is responsible for fetching the data, caching results and load the data into our components. It also handles load states and error states.

Storefront specifically uses [vue-apollo](https://github.com/Akryum/vue-apollo).

Here's a small example of a component that fetches a list of products from Shopify using `vue-apollo`.
```
<template>
    <div class="products">

        <h2>Products</h2>

        <div v-if="$apollo.loading">
            Loading...
        </div>

        <ul v-if="products">
            <li v-for="product in products" v-text="product.title"></li>
        </ul>
    </div>
</template>

<script>
    import { GET_PRODUCTS } from '../grapql/queries'

    export default {

        apollo {
            products {
                query: GET_PRODUCTS,
            }
        } 

    }
</script>
```
As mentioned earlier, `vue-apollo` handles load, error and success states. In our component we have acces to the `$apollo` object, where we can check it it's actively loading. 

In our script we have defined a query for products. The `GET_PRODUCTS` constant is a GraphQL query as described in the [GraphQL section](/docs/{{version}}/graphql). When data is return it will automatically be populated into the `products` variable, and can be used in our component. 

This is a slightly simplified example but this is the basic idea of how `vue-apollo` works. 
