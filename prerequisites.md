# Prerequisites

- [Vue](#vue)
    - [Slots](#slots)
    - [Router](#router)
- [GraphQL](#graphql)
- [Shopify](#shopify)
- [Storefront API](#storefront)

<a name="vue"></a>
## Vue
[Vue](https://vuejs.org/) is a Javascript framework. It has gained a lot of traction in recent years. Vue allows you to write encapsulated components which are responsible for HTML, CSS and Javascript. Vue components can be plugged into static sites or into other Vue components, allowing for complex functionality. 

Storefront is built upon Vue so knowledge of Vue is strongly recommended before you start a new project. Luckily Vue is fairly simple to get started with.

You can learn more about Vue [here](https://vuejs.org/v2/guide/).

<a name="slots"></a>
### Slots
A more advanced feature of Vue is [slots](https://vuejs.org/v2/guide/components.html#Content-Distribution-with-Slots). Understanding how to use slots is important since Storefront use them quite a lot. 

The basics of slots is that it's a placeholder in your component, you can then modify when you use the component. Why is this useful? Well, let's look at an example. 

In this example we have a `Card` component. The `Card` consists of an image and some text. 
```
<template>
    <div class="card">
        <div class="card--image">
            <img src="http://via.placeholder.com/500x500" />
        </div>
        <div class="card--content">
            <h3>A title goes here</h3>
            <p>
                Lorem ipsum dolor sit amet...
            </p>
        </div>
    </div>
</template
```
And it can be used like this
```
<card></card>
```

But now all the content is static. If we ever want to use the `Card` component in another place in our app, we would have to create an `AlternativeCard` component. 

This doesn't scale very well though. So let's instead make our `Card` dynamic.
```
<template>
    <div class="card">
        <div class="card--image">
            <img :src="image" />
        </div>
        <div class="card--content">
            <h3>{{ title }}</h3>
            <p>
                {{ content }}
            </p>
        </div>
    </div>
</template

<script>
    export default {
        props: ['image', 'title', 'content']
    }
</script>
```

Now when we use the `Card` component we will give it some data.
```
<card
    image="http://via.placeholder.com/500x500"
    title="A title goes here"
    content="Lorem ipsum dolor sit amet..."
>
</card
```

This is definitly an improvement, but it's not perfect. First of all then it feels awkward to pass an entire paragraph as a prop to the component. But it also limits us quite a bit. What if we don't want to output all our content in a `<p>` tag? And what if we want to use other tags like headings, blockquotes etc.

This is where slots come in. Let's do a final refactor of the `Card` component. 
```
<template>
    <div class="card">
        <div class="card--image">
            <slot name="image"></slot>
        </div>
        <div class="card--content">
            <slot name="title"></slot>
            <slot name="content"></slot>
        </div>
    </div>
</template
```

Now whenever we use the `Card` component we can decide what goes into each slot.
```
<card>
    <img src="http://via.placeholder.com/500x500" slot="image" />
    <h2 slot="title">Our new title goes here</h2>
    <div slot="content">
        <p>
            Lorem ipsum dolor sit amet...
        </p>
        <h4>We have more content in this card</h4>
        <p>
            Lorem ipsum dolor sit amet...
        </p>
    </div>
</card>
```

As you can see this gives us quite a lot of flexibility when it comes to customizing components. 


<a name="router"></a>
### Router
Router

