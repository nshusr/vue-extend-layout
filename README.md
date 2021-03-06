# vue-extend-layout
A simple extend the default layout or create custom layouts for your SPA Vue.js, using dynamic import component.

> For vue-extend-layout version 1.* you can access [this link](https://github.com/ktquez/vue-extend-layout/tree/v1.1.3)

## [vue-cli-plugin-layouts](https://github.com/ktquez/vue-cli-plugin-layouts) (vue-cli 3)
You can easily add the vue-extend-layout in your vue-cli 3 project.

```shell
vue add layouts
```

You will be asked if you want the plugin to configure the component for you automatically, if you accept, the plugin will create the default layout in the `src/layouts/default.vue` directory and will convert your `App.vue` into a *wrapper* for the layouts, similar to this example (https://github.com/ktquez/vue-extend-layout#in-your-appvue)

---

## Others installations

**NPM**
```shell
npm install vue-extend-layout --save
```

**Yarn**
```shell
yarn add vue-extend-layout
```


## Create and Using layouts

First of all:
- Create a directory called `layouts/` inside the main directory of your application, usually it will be from `src/layouts/`
- Inside the layout directory create a layout called `default.vue`

For example:  
`src/layouts/default.vue`
```vue
<template>
  <div>
    <YourHeader />
    <YourSidebar />
    <div class="container">
      <router-view />
    </div>
    <YourFooter />
  </div>
</template>

<script>
  export default {
    name: 'defaultLayout'     // you can enter any name (optional)
  }
</script>

<style>
/* your style */
</style>
```

#### In your `App.vue`

```vue
<template>
  <div id="app">
    <vue-extend-layouts />
  </div>
</template>

<script>
import VueExtendLayouts from 'vue-extend-layout'

export default {
  name: 'App',
  components: { VueExtendLayouts }
}
</script>
```

## Custom extend layout
To create a layout you just need to create a component within the layouts directory and name that component.  

For example:
`src/layouts/auth.vue`

```vue
<template>
  <div>
    <header-login />
    <div class="container-login">
      <router-view />
    </div>
  </div>
</template>

<script>
  export default {
    name: 'MyNameComponent'   // you can enter any name (optional)
  }
</script>

<style>
/* your style */
</style>
```

And to extend this layout in any the desired route, simply include the property `layout: auth` in meta object of the route.
```javascript
{
  path: '/login',
  name: 'Login',
  component: () => import('@/pages/Login'),
  meta: {
    layout: 'auth'
  }
}
```

# Create a error layout (Optional)

For example:
`src/layouts/error.vue`

```vue
<template>
  <div>
    <h1>PAGE NOT FOUND</h1>
  </div>
</template>

<script>
  export default {
    name: 'error'       // you can enter any name (optional)
  }
</script>

<style>
/* your style */
</style>
```

And in the route add in the 'meta' object the 'layout' property with the name of the layout component, in this case 'error'.
```javascript
{
  path: '*',
  name: 'Error',
  // component: () => import('@/pages/Error') (Optional)
  meta: {
    layout: 'error' // name of the layout
  }
}
```

## Defining the directory path of layouts

Prop       | Data Type  | default     | Description
---------- | ---------- | ----------  | -----------
`path`     | String     | `layouts`   | The layout directory path without a slash at the end

```vue
<template>
  <div id="app">
    <vue-extend-layouts path="views/layouts" />
  </div>
</template>

<script>
import VueExtendLayouts from 'vue-extend-layout'

export default {
  name: 'App',
  components: { VueExtendLayouts }
}
</script>
```

In this example the layouts will be in `src/views/layouts`

# Loading layout

For pages that need to load ajax requests and that take a moment to load, you can define a custom layout for a loading effect. Working only reloaded page;

**Attn: Only works when the page refreshes.**

Prop       | Data Type  | default  | Description
---------- | ---------- | -------- | -----------
`loading`  | String     | `null`   | Set the loading layout for late routes

```vue
<template>
  <div id="app">
    <vue-extend-layouts loading="loading" />
  </div>
</template>

<script>
import VueExtendLayouts from 'vue-extend-layout'

export default {
  name: 'App',
  components: { VueExtendLayouts }
}
</script>
```

**In the above example, the webpack will load the layout `loading.vue`**

> See example: https://vue-layouts2.surge.sh/contact

# Layout prefix

Add a prefix, avoiding conflict between the components of the layout and its application.

It also gives you the ability to load layouts according to the user's choices and seasonality, such as loading layouts on commemorative dates, using a new or modified version of the application, internationalization defining a layout template for a particular country, and so on.

Prop       | Data Type  | default  | Description
---------- | ---------- | -------- | -----------
`prefix`   | String     |          | Set the layout prefix

```vue
<template>
  <div id="app">
    <vue-extend-layouts prefix="old-" />
  </div>
</template>

<script>
import VueExtendLayouts from 'vue-extend-layout'

export default {
  name: 'App',
  components: { VueExtendLayouts }
}
</script>
```

**For example, if the layout is `default.vue` and you add the prefix `old-` the webpack will load the `old-default.vue` layout**

> Example coming soon

# Contributing

- Check the open issues or open a new issue to start a discussion around your feature idea or the bug you found.
- Fork repository, make changes, add your name and link in the contributors session readme.md
- Send a pull request

If you want a faster communication, check out my blog [ktquez.com](https://ktquez.com) or find me on Twitter [@ktquez](https://twitter.com/ktquez)

Thank you for using!
