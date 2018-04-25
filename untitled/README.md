---
description: >-
  This page will briefly introduce RxSwift, FRP, and how this excellent
  framework make my daily development more efficient.
---

# What's RxSwift

RxSwift is one of the frameworks of functional reactive programming\(FRP\) in Swift.

Compared to OOP, which every iOS developer is familiar with as both objC and Swift are OO language,  FRP is quite new to us. \(ok, at least to me\)

I first time know about FRP in Swift is in 2016, after about 2 months survey, I decided to use FRP in my daily development. It really make my code more readable, testable and simple.

### Functional Programming?

{% page-ref page="basic-of-functional-programming.md" %}

### Reactive Programming?

{% page-ref page="basic-of-reactive-programming.md" %}

### So, FRP = FP + RP?

So far the answer is yes for my understanding.

More explanation from wikipedia: [https://en.wikipedia.org/wiki/Functional\_reactive\_programming](https://en.wikipedia.org/wiki/Functional_reactive_programming)

### Why RxSwift?

Because nowadays we are facing more and more situations under which we need to do tasks in async.  In the past,  we use **GCD**, **NSOperation** and other technique to achieve that. It works well, but sometimes make my code hard to read, especially when there are so many tasks need to fire in async, and the callback of each task usually make the situation worse. 

FRP handles async tasks well and easily prevent callback hells. 

Below is a simple example of chaining multiple api requests:

{% tabs %}
{% tab title="OOP" %}
```swift
func someAPICall(complete: (_ result: Bool) -> Void) {
    //doSomething
    result(true)
}

func anotherAPICall(complete: (_ result: Bool) -> Void) {
    //doSomething
    result(true)
}

func callAPIsInOrder() {
    someAPICall {
            anotherAPICall {
                //Finally complete, do something.
            }
        }
    }
}
```
{% endtab %}

{% tab title="RxSwift" %}
```swift
func someAPICall() -> Observable<Bool> {
    return Observable.just(true)
}

func anotherAPICall() -> Observable<Bool> {
    return Observable.just(true)
}

func fireRequestsInOrder() -> Observable<Bool> {
    return someAPICall()
            .flatMapLatest { self.anotherAPICall() } 
}

let disposeBag = DisposeBag.init()
fireRequestsInOrder()
    .subscribe(onNext:{
        //Do something
    })
    .disposed(by: bag)
```
{% endtab %}
{% endtabs %}

It's easy to tell the difference that when using RxSwift the code is：

* Flattened, no more callback hells.
* Clean and Readable.



