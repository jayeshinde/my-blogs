---
layout: post
title:  "What is New in Angular 10"
date:   2020-06-29 21:53:23 +0400
categories: angular web development
---
 


Version 10.0.0 is major relase that span the entire platform which includes  Material, CLI and framework.
> Having 2 major releases within year angular team kept the framework synchronized with latest version of Javascript and Typescript ecosystem.

#### Major Changes:

- TypeScript v3.9 Support
    - Since 3.9 comes with various performance improvements, Angular 10 is not backward compatible with TypeScript now.
    - TSLib has been updated to v2.0
    - TSLint has been updated to v6
- `Solution Style` **tsconfig.json** Files
    - Support to [`tsconfig.json`][tsconfig] was introduced by [TypeScript 3.9] [typescript3.9].
    - A new file called `tsconfig.base.json` is introduced, to have `tsconfig.json` at root.
    
    ```javascript
        {
            "files": [],
            "references": [
                {
                    "path": "./tsconfig.app.json"
                },
                {
                    "path": "./tsconfig.spec.json"
                },
                {
                    "path": "./e2e/tsconfig.json"
                },
                { // added newly
                    "path": "./projects/core/tsconfig.lib.json"
                },
                { // added newly
                    "path": "./projects/core/tsconfig.spec.json"
                }
            ]
        }
    ```
 -  Angular Package Format Changes
    - Angular Package Format now does not include `esm5` and `fesem5` distributions.

- BrowserList
    - Angular generates bundles based on the [Browserlist][browserlist] configuration provided in the root app folder. Angular 10 will look up for a `.browserlistrc` in your app, but fall back to browserlist if not found. The `ng update` command will rename the file for you. Default browser support for Baidu, Opera, Samsung, Android Chrome removed.
 
- Removed `ModuleWithProviders` without Generic Type. 
    - After Ivy, since `metadata.json` is not required, Angular checks the generic type for type validation.
    - Example
    ```javascript
    @NgModule({...})
    export class SomeModule {
        static forRoot(): ModuleWithProviders<SomeModule> {
            return {
                ngModule: SomeModule,
                providers: [...]
            };
        }
    }
    ```
- UnDecorated Base Classes Removed
    - If you have `Angular Decorator` or `Dependency Injection` then we need to decorate the base classes also.
    - Dependency Injection Example
        ```javascript
        @Directive()
        export abstract class AbstractSome {
            constructor(@Inject(LOCALE_ID) public locale: string) {}
        }

        @Component({
            selector: 'app-some',
            template: 'Locale: {{ locale }}',
        })
        export class SomeComponent extends AbstractSome {}
        ```
        Here Angular 10 will throw error 
        ```javascript
        The component SomeComponent inherits its constructor from AbstractSome, but the latter does not have an Angular decorator of its own. Dependency injection will not be able to resolve the parameters of AbstractSome's constructor. Either add a @Directive decorator to AbstractSome, or add an explicit constructor to SomeComponent.
        ```
- New Data Range Picker
    - Angular Material now have new date range picker constructed from `mat-date-range-input` and `mat-date-range-picker` components.

- Warnings about CommonJS imports
    - Use of CommonJS for dependency manager result in larger slower applications. 
    - It is now recommendable to use an ECMAScript module (ESM) bundle for your depedancies

- Optional Strict Settings
    - Angular 10 now offer more strict project setups at the time of setting up the workspace using `ng new --strict`.
    - Benefits of strict flags are : 
        - Enables strict mode in TypeScript
        - Turns the template type checking to Strict
        - Default bundle budget to be reduced by ~75%
        - Configure linting rules to prevent use of type `any`


[typescript3.9]: https://www.typescriptlang.org/docs/handbook/release-notes/typescript-3-9.html#support-for-solution-style-tsconfigjson-files
[tsconfig]: https://angular.io/guide/typescript-configuration#configuration-files
[browserlist]: https://github.com/browserslist/browserslist