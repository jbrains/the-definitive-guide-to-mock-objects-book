***NYI***

## Objects, Schmobjects!

I learned to program in procedural languages like BASIC, Pascal, and C. I grew up professionally working in object-friendly languages like Java, C++, and Javascript. This means that I've trained myself to organise code into objects, and as a result, when I write about design, I tend to frame my thoughts in the context of objects. **You can safely replace "object" with "module" throughout this book**, if you prefer. I haven't (as of May 2014) worked professionally in strongly functional languages, although I have played around with Haskell. I believe that my object-oriented design style leans towards the functional, and my functionally-literate&mash;see what I did there?&mdash;friends and colleague mostly agree with that assessment, so I feel quite confident that the ideas in this book extend to using functions (and families of functions) as modules, rather than objects. After all, what makes up an interface except for a family of function signatures and a contract for their behavior? Whether we make these objects or modules, they have the same expressive power.

I say all this to ask you not to run away because you do Clojure and objects "are so last decade". When I say "object", you think "module". When I say "interface", you think "method signature" or "protocol". If you do this, then I don't think you'll bristle at anything I say here.[^refund]

[^refund]: If you find it really terrible, then remember that you have 45 days to get your refund. No hard feelings.

## Handrolled Test Doubles or Libraries?

I so don't care. Do whatever makes you happy. I use libraries (JMock, rspec-mock, google-mock, whatever you've got) because I understand them, I don't mind their syntax, and it gives me uniform style throughout my code base. If you handroll your stubs, I don't mind. (On the contrary, handrolling stubs encourages segregating interfaces more.) If you handroll method expectations and the inevitable duplication never starts to bother you, then we'll have to have a talk.

***NYI***
