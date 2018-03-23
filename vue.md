# Vue
- [Slots](#slots)
- [Scoped Slots](#scoped-slots)
- [Router](#router)

<a name="vue"></a>
## Vue
[Vue](https://vuejs.org/) is a Javascript framework. It has gained a lot of traction in recent years. Vue allows you to write encapsulated components which are responsible for HTML, CSS and Javascript. Vue components can be plugged into static sites or into other Vue components, allowing for complex functionality. 

Storefront is built upon Vue, so knowledge of Vue is strongly recommended before you start a new project. Luckily Vue is fairly simple to get started with.

A simple Vue component could look like this:
```
<template>
    <div class="hamburger-nav">
        <button class="toggle-nav" @click="toggleNav">Menu</button>
        <nav v-if="visible">
            <a href="/home">Home</a>
            <a href="/about">About</a>
            <a href="/blog">Blog</a>
        </nav>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                visible: false
            }
        },
        
        methods: {
            toggleNav() {
                this.visible = !this.visible
            }
        }
    }
</script>

<style>
    .hamburger-nav {
        background-color: blue;
        // More styles
    }
</style>
```
There's a lot going on here. So let's break it down step by step.

First we can see that the component is broken in to 3 main parts. A template, a script and styles. The template is where we define our markup. The script is where we write our Javascript. Styles are where we write our CSS. Pretty simple, right? Now in this example we are using all three parts, but this is absolutely not required. You can have a component that simply consists of a template, or a component that is only a script.

In our template we have simple HTML. But there are some new concepts. On the button we have this attribute: `@click="toggleNav"`. This is Vue's way of adding event listeners. So all this code is doing is add a click event listener to the button. And when the button is clicked then call the `toggleNav` method. 

This method is defined in our script, inside the 'methods' object. We can see that this method updates a variable `this.visible`. This variable is defined in the `data` method. The data method returns an object of data that is available inside the component. So where do we use this data? In our template, on our `<nav>` element we have another new attribute. The `v-if` directive. This directive allows you to control whether an element should be visible. In our example we are using the `visible` variable. That means that if `visible = true`, then our component will be shown. 

The last thing to understand is that whenever the `visible` variable is updated, the template will automatically re-render. So when we call the `toggleNav` method and update the `visible` state, the component will automatically register this change, and update accordingly. This is called 'reactivity' and is a core concept to understand.

This is a simple example but there are more things to know about Vue. I recommend taking a look at the [documentation]((https://vuejs.org/v2/guide/)).

<a name="slots"></a>
### Slots
A more advanced feature of Vue is [slots](https://vuejs.org/v2/guide/components.html#Content-Distribution-with-Slots). Understanding how to use slots is important since Storefront use them quite a lot. 

The basics of slots is that it's a placeholder in your component, you can then modify when you use the component. Why is this useful? Well, let's look at an example. 

In this example we have a `Card` component. The `Card` consists of an image, a title and some text. 
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
</template>
```

And it can be used like this:
```
<card></card>
```
But now all the content is static. If we ever want to use the `Card` component in another place in our app, we would have to create an `AlternativeCard` component. This doesn't scale very well.

Let's instead make our `Card` component dynamic.
```
<template>
    <div class="card">
        <div class="card--image">
            <img :src="image" />
        </div>
        <div class="card--content">
            <h3 v-text="title"></h3>
            <p v-text="content"></p>
        </div>
    </div>
</template>

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
</card>
```

This is definitly an improvement, but it's not perfect. The first issue is that it's awkward to pass an entire paragraph as a prop to the component. But it also limits us quite a bit. What if we don't want to output all our content in a `<p>` tag? And what if we want to use other tags like headings, blockquotes etc.?

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
</template>
```

Now whenever we use the `Card` component we can decide what goes into each slot.
```
<card>
    <img 
        slot="image" 
        src="http://via.placeholder.com/500x500" 
    />
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

If you only have one slot you don't have to name it:
```
<template>
    <div class="card">
        <slot></slot>
    </div>
</template>
```
```
<card>
   <div class="card--image">
        <img src="http://via.placeholder.com/500x500" />
    </div>
    <div class="card--content">
        <h3>A title goes here</h3>
        <p>
            Lorem ipsum dolor sit amet...
        </p>
    </div>
</card>
```
<a name="scoped-slots"></a>
### Scoped Slots
Scoped slots are a certain type of slot where you pass data from the child component to the parent component. Let's have an example to illustrate it. We'll continue using our `Card` component.

In this example each component will have a 'Dismiss' button that will hide the component.
```
<template>
    <div class="card" v-if="visible">
        <slot></slot>
        <button @click="hide">Dismiss</button>
    </div>
</template>

<script>
    export default {
        methods: {
            data() {
                return {
                    visible: true
                }
            },

            hide() {
                this.visible = false;
            }
        }
    }
</script>
```
A few things have changed. We introduced a data variable that controls whether the component is visible. We alse created a method that can toggle this variable. 
Lastly we added a button that will trigger the 'hide' method.

But now we've run into the same issue we had earlier when figuring out the markup of the component. What happens if we want the 'Dismiss' button above the content in some components? Or if we want the button to be a small 'x' in the top corner? Or if we want another text?

So once again it would be easier if we could handle it from the parent component. But one major thing has changed this time. We don't want to recreate the 'hide' method and 'visible' variable in each parent component. We still want `Card` to be responsible for this. 

That's where scoped slots come in. It allows us to pass data from the child component to the parent component. In our example it would look something like this:
```
<template>
    <div class="card" v-if="visible">
        <slot hide="hide"></slot>
    </div>
</template>

<script>
    export default {
        methods: {
            data() {
                return {
                    visible: true
                }
            },

            hide() {
                this.visible = false;
            }
        }
    }
</script>
```
What we've done here is simply pass the hide function as a prop to the slot. Now we can use it like this:
```
<card>
    <div slot-scope="props">
        <div class="card--image">
            <img src="http://via.placeholder.com/500x500" />
        </div>
        <div class="card--content">
            <h3>A title goes here</h3>
            <p>
                Lorem ipsum dolor sit amet...
            </p>
        </div>
        <button @click="props.hide"></button>
    </div>
</card>
```
We can use the 'slot-scope' property to access the props that were defined on the slot in the child component. We now have complete control over how the component can be hidden. It's not only methods you can pass through to the parent component. It could just as easily be a some data or a computed property.

<a name="router"></a>
### Router
Router

