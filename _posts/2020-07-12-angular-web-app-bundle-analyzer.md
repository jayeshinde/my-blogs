---
layout: post
title:  "Angular Performance Analysis with Bundle Analyzer"
date:   2020-07-12 21:53:23 +0400
categories: angular web development
---

In large Enterprise, it become difficult to manage Angular PWA apps considering performance. Therefore this become vital to look where the code in the final build come from using Bundle Webpack Analyzer.
- Performance is all about Improving Conversions
- Performance is all about Retaining the Users
- Performance is all about the User Experience
- Performance is all about People

> Web performance is possibly one of the most important parts to take into account for a modern web application. It plays major role in the success of any online venture. Here are some case studies that show how high-performing sites engage and retain users better than low-performing ones:

- [Pinterest][pininterest] increased search engine traffic and sign-ups by 15% when they reduced perceived wait times by 40%.
- [COOK][cook] increased conversions by 7%, decreased bounce rates by 7%, and increased pages per session by 10% when they reduced average page load time by 850 milliseconds.

Angular Web Pack Bundle Analyzer acts as X-Ray for your application, where one can identify the potential problem to increase in the bundle. Understand what you can do to make it smaller and further-optimized. The webpack-bundle-analyzer tool is perfect for this!

#### Configuration Steps:

![alt text](https://github.com/jayeshinde/my-blogs/blob/gh-pages/img/ang-webpack.png "BundleAnalyzer")

Head over to `app.component.ts` and `import` these into our `main.js` bundle:

```javascript
    import { Component, OnInit } from '@angular/core';
    import * as moment from 'moment';
    import * as firebase * from 'firebase';

        @Component({
            selector: 'app-root',
            templateUrl: './app.component.html',
            styleUrls: ['./app.component.scss']
        })
    export class AppComponent  implements OnInit {
        ngOnInit(): void {
            const time = moment.utc();
            const firebaseConfig = {};
            firebase.initializeApp(firebaseConfig);
        }
    }
```

Bundle has gone from about 9kB to 24kB. We should analyze this to see what we can do to get this lower. We will be installing now the webpack-bundle-analyzer plugin:

```javascript
    $ npm i webpack-bundle-analyzer -D
```

- Analyzing with `Stats.json`
We can make another script which runs the `webpack-bundle-analyzer` with the `stats.json`:

```javascript
"scripts": {
  "analyze": "webpack-bundle-analyzer dist/AngularBundleAnalyser/stats.json"
}
```

- Run the analyzer with the following command:
```javascript
$ npm run analyze
```

We then be able to see your analysis over at localhost:8888:

```javascript
Webpack Bundle Analyzer is started at http://127.0.0.1:8888
Use Ctrl+C to close it
```

![alt text](https://github.com/jayeshinde/my-blogs/blob/gh-pages/img/webpack-bundle-analysis.png "BundleAnalyzer")

[pininterest]: https://medium.com/@Pinterest_Engineering/driving-user-growth-with-performance-improvements-cfc50dafadd7
[cook]: https://www.nccgroup.trust/globalassets/resources/uk/case-studies/web-performance/cook-case-study.pdf
