With [Vue Router](https://router.vuejs.org/installation.html), you can use its
`router.push()` function to programmatically navigate between routes on your site.

```javascript
const router = new VueRouter({
  routes: [
    {
      path: '/home',
      component: { template: '<h1>Home</h1>' }
    },
    {
      path: '/about',
      component: { template: '<h1>About Us</h1>' }
    },
    {
      path: '/user/:id',
      name: 'user',
      component: { template: '<h1> Your id is {{$route.params.id}} </h1>' }
    }
  ]
});
  
const app = new Vue({
  router,
  methods: {
    changeRoute(route) {
      router.push(route);
    }
  },
    template: `
    <div id="rendered-content">
      <div>
        <button @click="changeRoute('home')">Home</button>
        <button @click="changeRoute('about')">About Us</button>
        <button @click="changeRoute({path: '/user/123'})">Get ID</button>
      </div>
      <div>
      <router-view></router-view>
      </div>
    </div>
  `
}).$mount('#example');
```

You can also pass a location descriptor object like `{path: 'home'}` into the `router.push()` function to achieve the same result.

## Passing Parameters

To pass parameters using `router.push()`, you can do one of the following:

```javascript
router.push({ name: 'user', params: {id: 123}});

// or

const id = 123;
router.push({ path: `/user/${id}` });
```

To then access it, use whatever you declared in the router as the object property name.
If the route was `/user/:id` the path would be `$route.params.id` or you could access
it as a prop by adding a `props:true` object in the route.

```javascript
{
  path: '/user/:id',
  component: { template: '<h1>Your id is {{$route.params.id}}</h1>' },
  props:true
},
```


[Live Demonstration](/tutorials/vue/router/example2.html)

