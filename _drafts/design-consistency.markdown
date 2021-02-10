---
title: "Consistent Design"
lang: en
picture: https://s3.amazonaws.com/javieracero.com/consistent-design.jpg
excerpt: "Features in any product vary in complexity. Designing for the median complexity and reusing the design is not a cost effective practice."
layout: post
---

Consistency is usually a quality desired in the design of any system. Unfortunately it means different things depending on who you talk to. It is frequently interpreted as using a small set of reusable building blocks.

The promise _"Design By Building Blocks"_ makes is that one will be able come up with a design that suits all features of your application. This design will be the [silver bullet](https://en.wikipedia.org/wiki/Silver_bullet) one can refer to when adding any feature to the system. It will also become the standard by which you judge the architecture of any part of your product.

In most cases this "recipe" comes in the form of a prescribed set of layers, with a side of patterns and restrictions on how these layers communicate with each other. Base abstractions are also a frequent ingredient.


## Tackling the median complexity

Any modern application today will provide dozens of features to its users. Even an MVP in private beta will include a handful of them. Each feature will have its own level of complexity. In a well designed system the complexity of the software will reflect the complexity of the feature it provides.

At any given time a software product will be composed of a few simple features, several average-complexity features, and a small number of very complex ones. The distribution of feature complexity will likely resemble a normal one:

![Complexity-vs-Feature-Count-Distribution](https://s3.amazonaws.com/javieracero.com/consistent-design-feature-count-vs-comlexity-1.png)

In order to find the target design one focuses on the features that are close to the median-complexity. That guarantees that we are considering the biggest chunk of the system possible. We look into the commonalities these features have and infer the patterns and restrictions from them.


## Advantages

In theory, your entire system follows the same architecture. This comes with a few perks:
* The structure of new features should be known, even before working on them.
* It should be rather simple to introduce engineers to the system.
* Engineers can walk away from the codebase, and come back knowing what to expect.
* Maintenance costs should be minimised by the patterns and restrictions.
* The costs of introducing new features should be close to linear.


## Problems

While the promise of a sliver bullet is tempting, one should be aware of the dangers ahead.

### Over-engineering

The features on the left tail of the distribution suffer from over engineering. The simpler the feature the bigger the problem is. Boilerplate code and excessive indirection are some of the symptoms to expect. This usually complicates the maintainability of these features, making the harder to understand and modify.

![Complexity-vs-Feature-Count-Distribution-Left-Tail](https://s3.amazonaws.com/javieracero.com/consistent-design-feature-count-vs-comlexity-2.png)


### Under-engineering

The features on the right tail of the distribution tend to be the most problematic of all. Frequently the complexity of the problem to tackle outgrows the prescribed patterns. Bloated abstractions are a frequent indicator that tends to be the source of bugs and burden maintainability.

It is also very frequent that these features end up being where the consistency breaks. The bloated abstractions are overflown by complexity and engineers refactor it away ignoring the predefined set of building blocks. Usually the organization overlooks this situation, and believes that consistency is still in place.


![Complexity-vs-Feature-Count-Distribution-Right-Tail](https://s3.amazonaws.com/javieracero.com/consistent-design-feature-count-vs-comlexity-3.png)


### The price of consistency

Keeping the patterns and restrictions consistent across a code base is, by far, the biggest problem any company that attempts to come up with a building block-based consistent design will face.

As the feature count grows, it is bound to happen that the initially defined conventions are no longer a good fit for a bigger subset of the system. Maybe even some of the initial building blocks are pin-pointed as the cause of issues.

![Complexity-vs-Feature-Count-Distribution-Evolution](https://s3.amazonaws.com/javieracero.com/consistent-design-feature-count-vs-comlexity-4.png)

The time to evolve the design has come.

The colossal problem is that keeping the consistency requires a tremendous effort from the organization. The features that are suffering issues have to be updated. But, on top of that, every other feature in the system needs to evolve as the building blocks are refined. It doesn't matter if it has been working flawlessly and hasn't required any maintenance in years.

Facing the level of effort this enterprise will require, most companies will surrender to the original design. Design problems will be worked around, or even worse, overlooked. Bugs will start to pile up. Time to market and development costs of new features will grow. Engineers will burn out dealing with repetitive issues, not able to tackle the root problems without breaking the consistency of the design.


## A better approach to consistency

Rather than focusing on the pieces of the puzzle, focus on what you are trying to achieve with them. Decide what qualities you want your design to have, define them and make sure that those stay during the evolution of the system.

Some examples:
* Modifiability: The system is easy to understand, modify and evolve.
* Testability: The system design allows for thorough and easy automated testing.
* Scalability: The system design allows for the service to be scaled.
* Resiliency and fault tolerance: The system takes errors into consideration and handles them properly.
* Observability and auditability: The system provides information of what happens inside it.

In order to make sure the architecture exhibits these qualities as it evolves you can define _Fitness Functions_ to monitor them as described in [Building Evolutionary Architectures](https://www.amazon.es/Building-Evolutionary-Architectures-Support-Constant/dp/1491986360).

It is imperative to allow for incremental changes to happen, adapting to increasing complexity. These may or may not cross-pollinate between subsets of the system when needed, without explicitly enforcing it.

A small set of building blocks, patterns and restrictions are OK to begin with, but always take them with a grain of salt. Be flexible and allow for rules to be broken. That's were innovation starts.



