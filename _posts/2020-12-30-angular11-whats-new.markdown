---
layout: post
title:  "Angular 11 Whats New!!!"
date:   2020-12-30 21:53:23 +0400
categories: angular web development
---

Version 11.0.0 is major release which includes Router, Forms and added HMR Support(Hot Module Replacement).
> Having 3 major releases within year angular team not only kept the framework synchronized with latest version of Javascript and Typescript ecosystem, but tried to caters needs for broader developer community.

### Major Issues Fixes:

- [`Lazy Modules`][lazy-modules] in the Named Outlets
- [`routerLinkActive`][router-link] is not getting re-evaluated when its corresponding routerLink is updated
-  Not able to [`translate`][translate] strings used anywhere in the code, using an API
- [`Relative`][routerLink] links should be generated properly: /a and /b.
- [`statusChange`][FormGroup] should always be emitted on FormGroup and FormControl

### Important Web Vitals FCP: 
- Automatic Inlining of Fonts
 To make your apps even faster by speeding up their [`first contentful paint`][fcp], automatic font inlining has been introduced. This is default in the apps built with version 11.

### Component Test Harnesses
 [Component Test Harnesses][test] has been completed for all components in release 11. The parallel function makes working with asynchronous actions in your tests easier by allowing developers to run multiple asynchronous interactions with components in parallel. The `manualChangeDetection` function gives developers access to finer grained control of change detection by disabling automatic change detection in unit tests.

### Ivy-Based Language Service Preview
 
 The language service will be able to correctly infer generic types in [templates][ngFor] the same way the TypeScript compiler does.

### Hot Module Replacement (HMR) Support

By typing below command on the development server, one can enable the HMR in angular project.
```javascript
 ng serve --hmr
```

### Faster Assembly
Accelerating the development and build cycle by making updates in some key areas.
- Faster compilation with TypeScript v4.0.
- Experimental [Webpack][webpack] v5.4.0 Support


[lazy-modules]: https://github.com/angular/angular/issues/12842
[router-link]: https://github.com/angular/angular/issues/18469
[translate]: https://github.com/angular/angular/issues/11405
[routerLink]: https://github.com/angular/angular/issues/13011
[FormGroup]: https://github.com/angular/angular/issues/14542
[fcp]: https://web.dev/first-contentful-paint/
[test]: https://material.angular.io/cdk/test-harnesses/overview
[ngFor]: https://angular.io/guide/template-typecheck#checking-of-ngfor
[hmr]: https://webpack.js.org/guides/hot-module-replacement/
[webpack]: https://webpack.js.org/concepts/module-federation/