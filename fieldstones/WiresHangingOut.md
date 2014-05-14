# Disconnected Wires

Your controller tests expect a method named `errors`. Your model exports a method named `error`. All the tests pass, but you have the Chunnel Problem[^chunnel-problem]. Obviously, mock objects are dangerous and you're stupid. Right?

[^chunnel-problem]: You started building from both ends of the tunnel at once and the ends don't quite meet in the middle.

Well, you've made a mistake, and you've made it with mock objects, but that neither makes them dangerous nor you stupid. If I make a mistake often enough, I have to either stop doing whatever causes me to make the mistake or build systems to detect and correct the mistakes before they become too costly. As you might guess, I have a system for avoiding this exact kind of mistake in my code. This system happens to lead to other useful behavior.

***NYI*** Describe collaboration and contract tests. Use http://bit.ly/1srv1s3 as a starting point.

## Can I Get A Tool For That?

Don't let it become an Evil Wizard, but sure: starting in 2013 I saw people trying to build tools to detect mismatches between collaboration tests in one layer and contract tests in the one below. Ruby has `bogus`. Java has `junit-contract`. I haven't used any of them, but I applaud anyone for trying to solve this problem. I actually *like* the double-entry book-keeping aspect of having to maintain correspondence between the collaboration tests and the contract tests. Call me old-fashioned.




