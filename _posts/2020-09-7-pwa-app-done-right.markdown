---
layout: post
title:  "PWA Done Right"
date:   2020-09-07 21:53:23 +0400
categories: angular web development
---

Modern Desktop Browsers and JavaScript becoming more powerful now a days. Due to Corona Pendemic, entire world's IT Infrstructure put under test, where desktops, tablets become primary need. Material UI transformed the web experience which narrows the gap where OmniChannel experience put as primary need. 

### WHY PWA 
- Hardest problem with applications is distribution and maintainacne, where most of time of Developers/ Architects gets killed in this process.
- App works in offline mode, Users can create a short-cut icon in their home screen and launch.
- Web Push Notifications - Way to engage the users like Mobile Push Notifications


### Core Technologies
Most API’s in the PWA space are built on JavaScript Promises and the Fetch API. This video provides an explanation of these technologies, as well as a brief introduction to [ES2015][ES6].

### PWA Preperation
We’re going to add `@angular/pwa` to our bundle through AngularCLI which does the following:
- Adds the @angular/service-worker package to your project.
- Enables service worker build support in the CLI.
- Imports and registers the service worker in the app module.
- Updates the `index.html` file to include a link to the `manifest.json` file and adds the meta tags for `theme-color`. - Installs icon files to support the installed PWA.
- Creates the service worker configuration file called `ngsw-config.json`, which specifies the caching behaviours and other settings.
- Use this in your project folder:
`ng add @angular/pwa`

## Structure of PWA

### Manisfest.json
For a PWA to run, we need several extra files. First, we need a [`manifest.json`][manifest], which is the web app manifest: a simple JSON file that tells the browser about your web application and how it should behave when “installed” on the user’s mobile device or desktop.
Notable attributes in this manifest are `name`, `short_name`, `description`, `theme_color`, and `background_color`. Make sure these are properly entered. The short_name is used as name of your application when added to a home screen, so make sure to add it.

### Icons
The icons are more important than you think, so make sure you create them in the proposed sizes. If you’re practical, you can use one of the many online [`fav-icon`][favicon] generators available. Make sure icons of 192 x 192 pixels and 512 x 512 pixels exist, since these are used by Android to display the “Add to Home Screen” install prompt and used by the Microsoft Store to automatically index and package your app.
If you look in the `manifest.json`, you’ll see a node icons. Take note of the sizes there that are automatically generated. My advice is that you make sure you have suitable icons for all these sizes.

```javascript
{
  …
  "icons": [
    …
    {
      "src": "path/to/maskable_icon.png",
      "sizes": "196x196",
      "type": "image/png",
      "purpose": "any maskable" // <-- New property value `"maskable"`
    }
  ]
  …
}
```

### ngsw-config.json
As stated earlier, the `ngsw-config.json` contains the settings on how the Angular-CLI build process will create your service worker. The default config will basically consist of an index attribute, usually pointing to your index.html, and the assetGroups. With this last attribute you can specify which files will utilise a certain install or update strategy.

```javascript
{
  "index": "/index.html",
  "assetGroups": [
    {
      "name": "app",
      "installMode": "prefetch",
      "resources": {
        "files": [
          "/favicon.ico",
          "/index.html",
          "/*.css",
          "/*.js"
        ]
      }
    }, {
      "name": "assets",
      "installMode": "lazy",
      "updateMode": "prefetch",
      "resources": {
        "files": [
          "/assets/**",
          "/*.(eot|svg|cur|jpg|png|webp|gif|otf|ttf|woff|woff2|ani)"
        ]
      }
    }
  ]
}
```

### Install Strategy
This strategy is to tell the application how it should install the app on the user’s device. By default, the `ngsw-worker.js` has set the install strategy (installMode) to prefetch, meaning all files specified will be fetched while it’s caching the current version of the app. This is bandwidth-intensive but ensures resources are available whenever they’re requested, even if the browser is currently offline.

```javascript
{
  "name": "app",
  "installMode": "prefetch",
  "resources": {
    "files": [
      "/favicon.ico",
      "/index.html",
      "manifest.json",
      "/*.css",
      "/*.js"
    ]
  }
}
```
### Caching Asset

Caching Assets
Your assets are configured by default as assetsGroup assets. Again we have the prefetch and lazy strategies available.

```javascript
{
  "name": "assets",
  "installMode": "lazy",
  "updateMode": "prefetch",
  "resources": {
    "files": [
      "/assets/**",
      "/*.(eot|svg|cur|jpg|png|webp|gif|otf|ttf|woff|woff2|ani)"
    ]
  }
}
```

Notice that the installMode is set to lazy while the updateMode is set to prefetch, meaning that assets will be loaded on demand, but if an assets has already been cached it will be pro-actively updated. If you want to add assets from external servers or CDNs (like Google fonts), amend the resources like this:

```javascript
"resources": {
  "files": [
    "/assets/**",
    "/*.(eot|svg|cur|jpg|png|webp|gif|otf|ttf|woff|woff2|ani)"
  ],
  "urls": [
    "https://fonts.googleapis.com/**"
  ]
}
```

### Data Groups

Data Groups are different than assets in the sense that they are not packaged with the version of your app. They could, for example, come from an API. They can be cached with two different strategies: freshness and performance.
The freshness strategy is useful for resources that change frequently and you don’t want to show outdated data for. This strategy will always try to get a new version of the resource before falling back to the cache.

```javascript
"dataGroups": [{
  "name": "api-freshness",
  "urls": [ "https://my.apipage.com/user" ],
  "cacheConfig": {
    "strategy": "freshness",
    "maxSize": 5,
    "maxAge": "1h",
    "timeout": "3s"
  }
}]
```

This snippet will get data from the /user endpoint and will be cached for at most 1 hour, a maximum of 5 responses and a timeout of 3 seconds. After this it will fallback to the cache.
The performance strategy, the default strategy, is more useful for resources that don’t change a lot. It will always show the cached version of a resource if available, but this can obviously lead to staleness of the response.

### App Updates

Angular PWA provides the [`SWUpdate`][SWUpdate] service.
- This provides two events — `available` and `activated`.
By subscribing to these events, we now if the cached app is current or outdated.
There is a `checkForUpdate` method to check the server if there is an update.
This is required if you want to check for update on your own — even if user is not launching the app.
Then you have the `activateUpdate` method that will actually update the current app to the latest.
A good practice of PWA app would be to determine if there is an update and provide an option for user to update. To do this in an angular app, you could write a small service.

Forcing Update Activation Strategy 

```javascript
import { Injectable } from '@angular/core';
import { SwUpdate } from '@angular/service-worker';
@Injectable({
  providedIn: 'root'
})
export class AppUpdateService {
constructor(private readonly updates: SwUpdate) {
  this.updates.available.subscribe(event => {
    this.informUpdate();
  });
}

informUpdate() {
  this.updates.activateUpdate().then(() => document.location.reload());
}

}
```

- Add this service as a provider in your `app.module.ts`.
- Add this service in the constructor of your `app.component.ts`


[favicon]: https://realfavicongenerator.net/
[manifest]: https://web.dev/add-manifest/
[SWUpdate]: https://angular.io/guide/service-worker-communications
[ES6]: https://developers.google.com/web/shows/ttt/series-2/es2015