---
layout: page
---
### Reactive UIs with Angular 2.0

**WTF is Reactive?**

Yeah, really, what is up with this buzzword that keeps getting thrown around a lot? Isn't this like a server side thing that folks use to improve their server's throughput? Do you really have to get this to the UI as well? Really? Well, that's with this article is all about - about trying to understand the benefits of getting the 'reactive' concepts to the UIs.

If you look at the reactivex site [here](http://reactivex.io/) you'll notice they pitch *reactive programming* as a combination of best ideas from the iterable pattern, observable pattern and functional programming. And if you look at the [Reactive Manifesto](http://www.reactivemanifesto.org/), it pitches a *reactive system* as having the following characteristics - responsive, resilient, elastic and message driven.

So effectively, a reactive system is a system that is non-blocking and asynchronous. But wait, isn't javascript non-blocking and asynchronous by nature? It is. But a reactive system is also message driven. Duh, isn't javascript also message driven? It is. The fact that javascript is asynchronous means that concurrency is handled via message passing. But this message passing is an implementation detail - not something that developers consciously implement in their application code. I will refer you to MDN's article on [javascript's concurrency model](https://developer.mozilla.org/en/docs/Web/JavaScript/EventLoop) and this [excellent jsconf video](https://www.youtube.com/watch?v=8aGhZQkoFbQ) to get the lowdown on this topic.

Finally, it is not necessary but helps a great deal if your reactive system is *functional* instead of *imperative*. Functional programs specify *what* to do where as imperative programs have to specify the *how* as well. Having the ability to abstract away the *hows* in a highly asynchronous system and instead just focus on the *what* is a boon. It makes your code concise and more maintainable. So instead of just talking about how functional makes developers lives easier, lets take a look at a trivial example to demonstrate the succinctness of functional programming. How does all this relate to ng2 you ask? Patience padawan - we'll tie all this back to our heroic framework soon enough. (Not to come across as a condescending prick or a javascript jedi, but I always wanted to use that star wars reference).

The example that we'd be considering is a very trivial example. We want to find out the number of times a word ("sea") occurs in a given statement ("she sells six sea shells on the sea shore"). First up - the purely imperative way of doing things.

~~~
var statement = "she sells six sea shells on the sea shore";
var occurrenceCount = 0;
var words = [];

// split statement into words
var word = ""
for (var i = 0; i < statement.length; i++) {
    if(statement[i] !== " ") {
      word += statement[i];
    } else {
      words.push(word);
      word = "";
    }   
}

// calculate the count
for (var i = 0; i < words.length; i++) {
    if(words[i] === "sea") {
      occurrenceCount++;
    }
}

console.log(occurrenceCount);
~~~

Next up - purely functional way of doing things -

~~~
var statement = "she sells six sea shells on the sea shore";
var count = statement
    .split(" ")
    .map(word => (word.match(/sea/g) || []).length)
    .reduce((prev, curr) => prev + curr);

console.log(count);
~~~

Did I just use map and reduce? What is this? A tutorial on Hadoop? Well, map and reduce are not something exclusive to the realm of big data and can have [their origins traced to functional programming](http://www.cs.cornell.edu/courses/cs3110/2011sp/lectures/lec05-map-reduce/map-reduce.htm). So you see now the succinctness of code that results when you use functional paradigms? Hopefully this example has convinced you about the benefits of using a functional style to write your programs.

**Enter RxJS - Just what the doctor ordered**
So you are convinced about using a functional approach to build your next UI. Enter [RxJS](https://github.com/Reactive-Extensions/RxJS). There is also an excellent material on RxJS available [here](http://xgrommx.github.io/rx-book/index.html).  RxJS allows you to use functional constructs to build UIs that are reactive. You will likely come across this phrase across the Internet a lot -

~~~
RX = Observables + LINQ + Schedulers
~~~

You can completely ignore this for now. Instead, think of RxJS as a framework that operates on event streams. Events, by definition are asynchronous. Even in real life, occurrence of an event does not stop time. An event just occurs and time continues to move forward - that's asynchronous. Inside your web app, an event can be anything - a DOM event, an XHR event or even a custom event that is fired by one of your components. So now your web app can be thought of as a series of events (an event stream) to which your components can subscribe to and change their internal state accordingly.

Thinking of a UI as a composition of multiple state machines is a useful abstraction that multiple libraries and frameworks are converging to (redux, cyclejs, etc). But this post isn't about other libraries/frameworks, it is about angular - so lets get back to how RxJS can help us create composable state machines.

**Example - A completely useless aggregator**

To understand how angular 2.0 helps us write terse asynchronous functional code using RxJS, let us build a very useless aggregator of github issues. All this aggregator will do is make ajax calls to the github api and get a list of open issues for multiple repos. In this case - we will fetch the open issues for "angular", "material2" and "angular-cli" repos belonging to the "angular" org.

For this, we will have to write a method called "getOpenIssueCount" which gets a list of all the open issues for a specified repo and returns the count of these issues. Take a look at the ng1 and ng2 code side by side below -

~~~
// ng1 javascript
var getOpenIssuesCount = function(projectName) {
    var url = 'https://api.github.com/repos/angular/' + projectName + '/issues?state=open';
    var deferred = $q.defer();
    $http.get(url).then(function(res) {
        deferred.resolve(res.data.length);
    });

    return deferred.promise;
};
~~~

~~~
// ng2 typscript
getOpenIssuesCount(projectName: string) {
    var url = 'https://api.github.com/repos/angular/' + projectName + '/issues?state=open';
    return this.http
        .get(url)
        .map(res => res.json().length);
};
~~~

Notice how in ng2, I do not have to deal with promises. As opposed to ng1, ng2 http service returns an RxJS observable by default. This allows us to pretty much use any of the [RxJS' methods](http://xgrommx.github.io/rx-book/content/observable/observable_instance_methods/index.html) to operate on the response stream however we see fit. Now let us take a look at how we'd write out aggregate's code in ng1 and ng2

~~~
// ng1 javascript
var aggregateIssueCount = 0,
    promises = [],
    p1 = getOpenIssuesCount("angular"),
    p2 = getOpenIssuesCount("material2"),
    p3 = getOpenIssuesCount("angular-cli");

    promises.push(p1);
    promises.push(p2);
    promises.push(p3);

    p1.then(function(numIssues) {
        aggregateIssueCount += numIssues;
    });

    p2.then(function(numIssues) {
        aggregateIssueCount += numIssues;
    });

    p3.then(function(numIssues) {
        aggregateIssueCount += numIssues;
    });

    $q.all(promises).then(function() {
        $scope.count = aggregateIssueCount;
    });
~~~

~~~
// ng2 javascript
var angularIssueSource = this.getOpenIssuesCount("angular");
var materialIssueSource = this.getOpenIssuesCount("material2");
var angularCliIssueSource = this.getOpenIssuesCount("angular-cli");

angularIssueSource
    .merge(materialIssueSource)
    .merge(angularCliIssueSource)
    .reduce((x, y) => x + y)
    .subscribe(function(x) {
      self.count = x as number;
    });
~~~

Hopefully the above code samples do a decent job in contrasting the approaches ng1 and ng2 take when dealing with concurrency. In ng2, everything is a stream and you operate on those streams. This is a very powerful abstraction once you get the hang of it. Everything from keystrokes to mouse clicks to security events can be thought of as streams and your application code only operates on that abstraction. For a simple (and totally useless) aggregator, there is a visible decrease in the LoC. Imagine the gains in a complex enterprise UI with 100s of components communicating with each other, the user and a server - the benefits can be significant.

The entire code is available [here](https://github.com/ng1-vs-ng2/http-observables-vs-promises). This would be the first in a series of articles demonstrating the benefits of moving over to ng2.
