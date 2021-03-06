title: Coding Backwards
date: 2012-02-07 09:55
categories: python interface testing

At my real job I've been working in my spare time on a large-scale Python testing framework. When I decided our current framework didn't meet our needs, I took a new approach (for me) to developing software: _coding backwards_. Since doing so, I've learned that coding backwards can, _but not will_, lead to the creation of some fabulous APIs.

The idea for coding backwards was most clearly verbalized for me by
Aaron Swartz and his [web.py](http://webpy.org) framework. He says:
{% blockquote [Aaron Swartz] %}
 I wrote a web application in Python just imagining how I wanted the API
 to be. It started with import web, of course, and then had a place to
 define URLs, simple functions for GET and POST, a thing to deal with
 input variables and so on. Once the code looked right to me, I did
 whatever it took to make it execute without changing the application
 code -- the result was web.py. 
 {% endblockquote %}

This was a revelation for me. When you're building software for others
to use, __make it as natural as possible for them to do so__. I call
this _coding backwards_. It directly influenced how I built my testing
framework.

<!--more-->
I started with the finished product: a test script written in Python. I
wrote valid Python code against a library that didn't exist yet. Without
an existing API to get in my way, I was able to express my intentions
clearly. Anyone reading the test script would immediately know what was
happening. More importantly, they wouldn't be exposed to weird
implementation quirks. It was my version of the "optimal" test script for our system in Python.
After writing that script, there was only one problem: it didn't
actually do anything yet.

From the test script, I created the classes and functions that the test
script called. What I did within the library was less important than
_not changing the test script to fit the library_. If I have to make a
few weird implementation decisions as a result, fine. The point is,
__users are going to use the library's API, not the library's
internals__. Of course, that doesn't mean the implementation can be
spaghetti coded crap. It must be implemented professionally, just with
making the test script work as expected the primary goal.

Coding backwards prevents you from writing functionality that no one
will use, because someone is already using all of your library. That
keeps the interfaces tight and well defined. With something like a
testing framework, the interface is king. The ratio of test case writers
to test framework maintainers will be something like 10:1, so creating a
friendly, usable interface is key.

In actually writing the implementation, I found myself bouncing around
between the top level interface code and the lowest level library code
quite a bit. I would create a top level class or function, realize it
would need to call some library code, then go off and write that library
code. Again, though, I was coding backwards. I didn't start off writing
a bunch of low level libraries I thought I would need. I deferred
creation of the libraries until I actually needed them.

This lends itself well to writing tests. At each point, you're writing
the minimum required to get the interface working. Sounds suspiciously
like the methodology for creating unit tests. In practice, writing tests
naturally fit into the development flow. This is most decidedly _a good
thing_.

While the framework isn't complete, it certainly is usable. What's more,
it usable by just about anyone without having to even look at the
interface. Since I created the test script first, I have a wonderful
example to show the library's canonical use. I've been quite happy with
the results of coding the framework backwards. It puts emphasis on the
interface rather than the implementation, which is exactly where the
emphasis should be in a testing framework.

Questions or comments on _Coding Backwards_? Let me know in the comments
below. Also, [follow me on Twitter](http://www.twitter.com/jeffknupp) to see all of my blog posts and
updates.
