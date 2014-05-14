When I want to check an interaction and an output at the same time, I'm violating CQS, which might or might not be a problem in that specific case. I investigate.

When I want to check an interface, it's usually because I only have side-effects to check, and I don't want layer 3's tests polluted with assumptions about the way that layer 4 happens to behave this week. Example: controller should result in sending a message to the user, so in my controller test I check for sendMessage(recipient, body). This week, I send email. Next week, I send SMS. The week after, I send MMS. My controller shouldn't and doesn't change. Its tests shouldn't and don't change.

When I want to check output (like a return value), I don't typically want to check the interaction. Instead, I want to stub an interaction to return a convenient value so that I know what to expect. Example: I stub the model to return an empty set of Customers so that I know that my controller puts an empty set of Customers into the view under the key "customers".

Some objects are so simple that the tests duplicate the implementation. This will change over time as we add more features into that part of the code base.

When we have too much mock setup, that means that we have (1) too many collaborators, which points to a cohesion problem, which usually indicates a violation of SRP, which we fix by splitting the class in two; or (2) stubbing A to return a stub B, which we stub to return a stub C, which we stub to return a D with a certain value/in a certain state, which points to a clear layering problem, specifically indirection without abstraction, or a Law of Demeter violation, which we fix by introducing a useful abstraction.

When adding a new feature causes me to change a mock expectation, that tells me that a new abstraction is being born, so I introduce it. This nudges the code ever closer to respecting the Open/Closed Principle. Typically only two or three nudges are needed to stabilise a module enough to close it.
