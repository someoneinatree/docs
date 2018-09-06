# Story & Solution Design Process Brief

## 2-step process (iterable?)

What needs does our solution need to satisfy (and what needs does our solution have?)
1. Define each actor, and:
   * What they have at the beginning (e.g. data, products, money, etc)
      * Defining the beginning, and what these "haves" are can be confusing, so consider starting somewhere unambiguous and high-level, like "as a user on the webpage of a tour i want to go on, i want to use an application that takes my (x, y, z), and gives me..."
   * What they want at the end (e.g. products, information)
2. Flow diagram (i.e. process/data sequence flow)
   * An expression of interactions between the actors, refering to what they have, decisions available to them (i.e. flagging logical branches in flow)
   * Can introduce services (e.g. APIs) as actors, i.e. all actors have "APIs" (a set of indexed, documentable functions with each some 1) required input and 2) expected output)
      * Potentially, projects may be described by a single (or smallest possible number) of exhaustive happy path(s), and where all fail paths between happy paths are tested before advancing. Stories then mostly target single attributes (or sets of elements) of those request/interactions
         * A "path" being a simple ordered list of interactions, where an interaction is conversation between two Actors with a specified format of Input -> Output (when interacting with external APIs the dev work means modifying one Actor i.e. writing a request, but internally there is some )
   * Each step below the top level of software spec is in a level of "solutionizing". Keeping track of data flow, which systems are responsible for which things, is a good way of noticing when approaches change. The aim should be to define levels downwards until you get to specifying your software, its set of endpoints and the input/output/side effects it expects to recieve/deliver/produce.

Naively, a piece of deliverable software looks something like:
```
Deliverable = (config | environment) => App({
	[`/route`, `function`].oneOf(): (...dataInput) => { ...dataOutput },
	[... ""]: (...dataInput) => [{ ...dataOutput }] // { ...sideEffectsOnServices }
})
```
...or, a Deliverable is an executable/function that takes some environment/config and instantiates (or as in serverless approaches has a method of dynamcally instantiating) an App, which has an index of routes/functions with specified patterns of input and output (each with a set of expected side effects on services provided by the environment)

## Example

For the case of LionWorld, step 1 might look like the following:
* Actors:
   * Lionworld (has: bookings to sell, wants: sold bookings)
   * TTC-Payment Services (has: cybersource integration)

## Random Thoughts

* "Naive customer" - fallacy that a customer's story can't be described using terms the customer wouldn't deal with. Story "as an X I want Y" is confusing for this reason - the implementable description of Y will always refer to the effects on another system, be it what gets output to the customer, what changes in a database, or some combination. E.g. "as a customer, i want to have a paid booking entry in tropics database so that i can go on holiday". the customer doesn't know all this, but it's true in quite a pure way that describes the acceptance criteria for that journey. This makes sense, because the "so that I can..." part of a story will often be unintelligible to the described actor, given it describes something that *other actors* currently aren't doing that named actor *wants* them to do. Thinking like this, data flow is a list of statements like: `Actor performs action(: act/input => reaction/output)`. Thus: Stories modify Actors in a way that allows them to perform more actions within the various paths, until all actions perform as expected. Tasks modify actors in one-time ways without side-effects.