---
layout:     post
title:      "Ember Components and Injection"
subtitle: "Ember is awesome. Components are awesome. Injection is awesome. Read this - its awesome"
author:     "Dan"
header-img: "img/post-bg-05.jpg"
---
The Problem
--
The move from Ember views and controllers to Ember routable components has been full of aggravation for many developers. The
biggest issue is that while we know controllers are being phased out
in favor of routable components, we are still forced to heavily use
controllers in order to work with the data store and to handle
redirecting to other pages in the app as a result of actions.

The Solution
-- 
In Ember 2.* we can solve both of these problems using injection.

The first issue is fixed by simply adding `store: Ember.inject.service()` into our component and then accessing by using `this.get('store').findAll(article)`. You now have the same access to
the store as you would from a controller in a completely isolated component.

The second issue is fixed by globally injecting the router into our components. If you don’t already have one, add the folder `app/initializers`. In there, add a file called `component-router-injector.js` and add in the following code:

```
// app/initializers/component-router-injector.js export function initialize(application) { // Injects all Ember components with a router object: application.inject('component', 'router', 'router:main'); }

export default { name: 'component-router-injector', initialize: initialize }; 
```

We can then call our router from any component by doing this: `this.get('router').transitionTo('dashboard'))`.
