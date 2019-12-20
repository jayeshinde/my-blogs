---
layout: post
title:  "Say No to Storyboards - Top 10 Reasons"
date:   2019-12-19 21:53:23 +0400
categories: swift interview questions
---
As a Passionate iOS Developer, working more than a Decade in Mobile technologies and its integration with different enterprise platforms like SAP, Salesforce, IBM Mainframe, MS Sharepoint, AWS Cloud. Managing such large scale Enterprise or Custom Facing iOS Native apps is key challenges organizations are facing. Today, I will tell **Top 10 Reasons - Say No to Storyborards.**

`Why to Say No (In Dilemma whether to use Storyboard or Not):`

- Apple introduced new [SwiftUI][swiftui]
- There is shift in programming paradimes from Imperative to Declerative
- Maintain large apps with more number of Storyboards becoming bottlenecks to prevent use of CICD, adopt new programming paradimes, upgrade iOS native apps.

`Top 10 Reasons`

10. [Storyboard][storyboard] uses XML which follows Apple own propertiery schema. While working with large teams of developers, with multiple storyboards, managing the merges issues becomes headache, especially when more than single person working on the same storyboard. Thus decrease in productivity.
9. Storyboards has small windows to manage which makes difficult to have fine grain precision, especially in conditions where there are more than 10 views or contorls.
8. Storyboards follows Target-Action Pattern which makes difficult to test large app.
7. Dramatic Increase in the Compile time of project observed when working with storyboards, more than 100.
6. Refactoring of element within storyborads observed quite complex and tedious especially there are heavy fonts, styling, multilingual, deep localization.
5. Storyboards are identified using *[StringIdentifiers][segue]*, which makes difficult to maintain routing or navigations in dynamic workflows scnerios.
4. IBOutlet and IBActions causes viewcontrollers difficult to tests, thus reducing the code coverage. IBOutlet and IBActions causes app to have run time crash if any one of the linkage is missed.
3. Layouting the Subviews become tedious when dealing with Universal apps, where multiple storybords needs to mainatain for watch, ipad, iphone.
2. Migrating to new XCode or Migrating to new APIs, its become difficult to find deprecated apis in terms of layouts, fonts, colors, etc. Storyboard causes UIWindow object to be aviable by default which makes difficult to manage.
1. Apple is shifting towards Scence Deleagte where UIWindow become optional and UIScence is controlling the rendering. ( Scene Delegate, by default sets up a UIWindow object)

[swiftui]: https://developer.apple.com/xcode/swiftui/
[storyboard]: https://developer.apple.com/library/archive/documentation/ToolsLanguages/Conceptual/Xcode_Overview/UsingInterfaceBuilder.html#//apple_ref/doc/uid/TP40010215-CH42-SW1
[segue]: https://developer.apple.com/documentation/uikit/uistoryboardsegue/1621909-identifier
