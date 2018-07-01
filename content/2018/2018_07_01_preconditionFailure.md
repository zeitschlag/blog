Title: preconditionFailure
Date: 01.07.2018, 22:08
Tags: [swift, pragmaticprogrammer]
Lang: en

One of my goals for May 2018 was to finally read [The Pragmatic Programmer](https://pragprog.com/book/tpp/the-pragmatic-programmer). I haven't succeded yet, that's why this year, June was May, Extended Edition and July is June, Extended Edition.

A few years ago, a dear friend of mine recommended reading this book to me and I should have listened to him. It is so interesting to read, I've learned a lot of things and I'm barely halfway through. What I like about this book is that it encourages you to think about your work and how you achieve it. It shows you good practices without being arrogant.

As I'm reading this book quite intensively, I take a lot of notes. If you're interested to read them, I'd be more than happy to publish them in another blogpost. [Just let me know](https://twitter.com/zeitschlag). At the moment, they're written down in my old-fashioned notebook.

In "The Pragmatic Programmer", there are several advices. Number 31 of them is:

> Design by Contract.

One of several things written down in a contract are preconditions. They're basically requirements or conditions, that one party must ensure to be true, before the other party can start to fulfill its part of the contract. It is to be defined in the contract, which party must ensure, that these requirements are met.

I am an iOS developer for a living. A few months ago, a former collegue of mine showed me [`assert`](https://developer.apple.com/documentation/swift/1541112-assert), [`assertionFailure`](https://developer.apple.com/documentation/swift/1539616-assertionfailure), [`precondition`](https://developer.apple.com/documentation/swift/1540960-precondition) and [`preconditionFailure`](https://developer.apple.com/documentation/swift/1539374-preconditionfailure).

The main difference — he explained it to me at least this way — was that `assert(false)` and `assertionFailure` let the app crash only in debug-builds, while a `preconditionFailure` leads to a crash in release-builds as well

When I read about preconditions in "The Pragmatic Programmer", I felt like being reminded about this conversation between my coworker and me. So I read Apple's documentation of [`preconditionFailure`](https://developer.apple.com/documentation/swift/1539374-preconditionfailure) again. It says:

> Indicates that a precondition was violated.
>
> Use this function to stop the program when control flow can only reach the call if your API was improperly used.

Next, I wanted to know, if Swift has some kind of *Design by Contract* support, but the mighty Internet [says no](https://stackoverflow.com/questions/31817359/design-by-contract-in-swift#31951965):

![](https://media.giphy.com/media/utmZFnsMhUHqU/giphy.gif)

The meaning of Apple's `precondition` and `preconditionFailure` differs slightly from *DbC*, just like the way they want me to use them: 

> The global functions `assert`, `assertionFailure`, `precondition` and `preconditionFailure` are designed to be sprinkled liberally throughout code without impacting release build performance. — [Source](https://stackoverflow.com/a/31951965/5626642)

So, yeah, as a conflusion one could say, that `precondition` the *DbC*-way seems to be different from *swifty* `precondition`.

Another thing I'd like to mention is, that I'd like to write more blogposts like this: somehow programming-related, short articles in english. I'm not entirely sure about the format: Should I just use this — German — blog? Should I start another one? What are your thoughts on this?
