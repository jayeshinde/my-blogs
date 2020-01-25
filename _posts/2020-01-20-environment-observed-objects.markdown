---
layout: post
title:  "@EnviornmentObject to share data between views"
date:   2020-01-25 21:53:23 +0400
categories: swift interview questions
---
SwiftUI to share data between the Views 

`Struggling to share data between views in SwiftUI?`

- Apple introduced new [SwiftUI][swiftui].
- There is shift in programming paradigm from Imperative to Declarative.
- Autoupdating the view whenever there are changes in the model.

SwiftUI provides way to share data across all views within app, using `@EnviornmentObject`. This enables the app to update the views automatically whenever data changes. 

#### Scenerios:
- If we want to pass data from A -> B -> C, instead of creating protocols or singleton objects, we can create `@EnvironmentObject` and put into the environment object so that views B, C and D can automatically have access to it.

#### Precaution:
- Environment objects must be supplied by an ancestor views, if wont find the object, it may lead to crash.

#### Usage:
- Object or Model that needs to be shared across views must confirms to protocol [ObservableObject][observableobject].
- Change in the model also communicated with the help of [@Published][published] property wrappers.

By default an `ObservableObject` synthesizes an objectWillChange publisher that emits the changed value before any of its `@Published` properties changes.

`Example`

{% highlight swift %}
 class Contact: ObservableObject {
    @Published var name: String
    @Published var age: Int

    init(name: String, age: Int) {
        self.name = name
        self.age = age
    }

    func haveBirthday() -> Int {
        age += 1
        return age
    }
}

let john = Contact(name: "John Appleseed", age: 24)
john.objectWillChange.sink { _ in print("\(john.age) will change") }
print(john.haveBirthday())
// Prints "24 will change"
// Prints "25"
{% endhighlight %}

[swiftui]: https://developer.apple.com/xcode/swiftui/
[published]: https://developer.apple.com/documentation/combine/published
[observableobject]: https://developer.apple.com/documentation/combine/observableobject
