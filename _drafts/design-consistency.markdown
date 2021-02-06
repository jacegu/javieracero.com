---
title: "Consistent Design"
lang: en
picture: https://s3.amazonaws.com/javieracero.com/consistent-design.jpg
excerpt: "Features in any product vary in complexity. Designing for the median complexity and reusing the design is not a cost effective practice."
layout: post
---

The promise that _Consistent Design_ makes is that one will be able come up with a design that suits all features of your application. This design will be the [silver bullet](https://en.wikipedia.org/wiki/Silver_bullet) one can refer to when adding any feature to the system. It will also become the standard by which you judge the design of any part of your product.

In most cases this "recipe" comes in the form of a prescribed set of layers, with a side of patterns and restrictions on how these layers communicate with each other.


## Tackling the median complexity

Any modern application today will provide dozens of features to its users. Even an MVP in private beta will include a handful of them. Each feature will have its own level of complexity. In a well designed system the complexity of the software will reflect the complexity of the feature it provides.

At any given time a software product will be composed of a few simple features, several average-complexity features, and a small number of very complex ones. The distribution of feature complexity will likely resemble a normal one:

![Complexity-vs-Feature-Count-Distribution](https://s3.amazonaws.com/javieracero.com/consistent-design-feature-count-vs-comlexity-1.png)

In order to find the target design one focuses on the features that are close to the median-complexity. That guarantees that we are considering the biggest chunk of the system possible. We look into the commonalities these features have and infer the patterns and restrictions from them.


## Advantages

In theory, your entire system follows the same structure. That should come with quite a few perks:
* The structure of new features should be known, even before working on them.
* It should be rather simple to introduce engineers to the system.
* Engineers can walk away from the codebase, and come back knowing what to expect.
* Design efforts should be minimised by the patterns and restrictions.


## Problems

While the promise of a sliver bullet is tempting, one should be aware of the dangers ahead.

### Over-engineering

The features on the left tail of the distribution suffer from over engineering. The simpler the feature the bigger the problem is. Boilerplate code and excessive indirection are some of the symptoms to expect. This usually complicates the maintainability of these features, making the harder to understand and modify.

![Complexity-vs-Feature-Count-Distribution-Left-Tail](https://s3.amazonaws.com/javieracero.com/consistent-design-feature-count-vs-comlexity-2.png)


### Under-engineering

The features on the right tail of the distribution tend to be the most problematic of all. Frequently the complexity of the problem to tackle outgrows the prescribed patterns. Bloated abstractions are a frequent indicator that tends to absorb bugs and burden maintainability.

![Complexity-vs-Feature-Count-Distribution-Right-Tail](https://s3.amazonaws.com/javieracero.com/consistent-design-feature-count-vs-comlexity-3.png)

It is also very frequent that these features end up being where the consistency breaks. The bloated abstractions are overflown by complexity and engineers refactor it away ignoring what _Consistent Desing_ dictates. Usually the organization overlooks this situation, and believes that consistency is still in place.


### The price of consistency

Keeping the patterns and restrictions consistent across a code base is, by far, the biggest problem any company that attempts to come up with a _Consistent Design_ will face.

As the feature count grows, it is bound to happen that the initially defined conventions are no longer a good fit for a majority of the features. Maybe even some of parts of the original design are pin-pointed as the cause of issues in the system. The time to evolve the design has come.

![Complexity-vs-Feature-Count-Distribution-Evolution](https://s3.amazonaws.com/javieracero.com/consistent-design-feature-count-vs-comlexity-4.png)

The colossal problem is that keeping the consistency requires a tremendous effort from the organization. The features that are suffering issues have to be updated. But, on top of that, every other feature in the system needs to evolve. It doesn't matter if it has been working flawlessly and hasn't required any maintenance in years.

Facing the level of effort this enterprise will require most companies will surrender to the original design. Issues will be patched, or even worse, overlooked. Bugs will start to pile up. Time to market and development costs of new features will grow. Engineers will be frustrated.

All of it sacrificed in the altar of consistency...
