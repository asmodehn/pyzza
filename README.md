# pyzza
Pyzza : Yaml Zoo of Zealot Agents. An asynchronous polyglot programming language experiment...

## Simplicity - As simple as possible, but not simpler.
Since we focus on concurrency here, and try to derive a way to describe "real world information systems", we need to limit ourselves in multiple ways :

- We will restrict ourselves to one corner of the [lambda cube](https://en.wikipedia.org/wiki/Lambda_cube) : the [simply typed lambda calculus](https://en.wikipedia.org/wiki/Simply_typed_lambda_calculus). This is enough to get Turing completion and the scope isolation prevent harmful state sharing between multiple flow of execution. Also simple type theory is simple, powerful and well understood from a pure theory perspective. Be careful however, currying is invalid when not dealing with pure lambda functions (such as those that interract with the real world).

- We will limit our data structures in what [YAML](http://yaml.org/) provides. Trees and references are enough to express most of basic data structures nowadays, and match what is already available in most languages. For example even a data graph in C++ would be represented with a tree (one-way ownership) going downward plus some weak references going upwards.

- We should leverage existing programming languages, as simply as possible, in order to implement only the strict minimum until we get some meaningful technical demonstration.

- We need a clear, open way to specify the language. that specification should be a documentation (YAML) that also gets tested automatically against the code for every change. Therefore it should be the goal that the YAML code itself is used as its specification... this means we need a solid theoritical background. Simply typed lambda can provide this.

## Reflexivity - Data is code, Code is Data.
The language should be [reflexive](https://en.wikipedia.org/wiki/Reflection_(computer_programming)).
One main reason of attempting the creation of a new language is that the dichotomy of write -> run these days is falling apart. Wirting server code, while server is permanently running, answering test request, is becoming more common.
Platforms like erlang OTP have been allowing [hot code swapping](http://arhipov.blogspot.kr/2009/07/nice-features-in-erlang-hot-code-swap.html) for a long while now.

This means that each piece of code need to have it's own version, and the user of a piece of code can specify a specific version to use.

This also means that the language itself needs to have its own version, and any program can specify which version it wants to use ( a little bit like a server would provide multiple versions of the same API )

The core of the language itself need his version, and needs to be used to derive any "higher level construct" in such a way that when the core of the language version changes in a compatible way, the "higher level constructs" also improve...

This also implies that the language needs to be proofed, if possible, or at least "fully automatically tested". A live editor would be a useful first tool for this.

## Asynchronicity - Let if flow !
The main idea is to make asynchronous & distributed programming ( which is a recent concept ) simple for any developer who has some experience in an existing mainstream language.

This means things like process/thread, coroutines, asynchronous call, futures/promises, etc. need to be core part of the language. How we do it remains to be seen... but we probably need some kind of Monad concept early on.

## Polyglotism - 
However we also want to be able to do what other languages already do and integrate this easily. The main idea here is to describe what we need from the other language in some YAML syntax, maybe similar to what ansible modules provides, in a top -down fashion.

But this needs to be available also in a bottom-up fashion, where a developer in another language can produce a yaml structure that is enough for other Pyzza agents to recognize and integrate it in their distribution information system.

It also means that it should be easy to integrate with other language or platform packaging systems...

## Property-based testing
Until we implement a complete [calculus of constructions](https://en.wikipedia.org/wiki/Calculus_of_constructions) and are able to completely proof the language, it is good to let the computer test as much as possible, and try to base this test on mathematically sound theoritical concepts.

These tests should run automatically, when any code version gets incremented while someone is writing/executing code.

## Deltas

In order to optimize distributed program, it is important to make it simple to manipulate differences/derivative instead of raw states. This optimisation is possible only if the message delivery is guaranteed between two agents. otherwise we need to transfer the full state everytime.

But that means that working with derivative values and deltas should be as simple as possible (in distributed systems like neural networks, it is the basis of the distributed learning algorithm).

This also means that merge algorithms for any data structures, should not be ambiguous. This can be a tricky challenge, especially regarding our optimistic concurrency control (requiring cancel and replay) and how we can order asynchornous events only partially (we do not know who should change that value in that structure).
