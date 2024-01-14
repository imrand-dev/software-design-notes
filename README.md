## Core Design Principles for Software Developers

### What's a good design?

> A design is good if the cost of changing is minimal.

- Correct solution takes iterations, constantly in evolution.
- Almost Impossible to get it right the first time.
    - Writing code first time is an exploration: many relationships are discovered, and questions are asked and answered.
- Software is never written, it's always rewritten.
    - When we’re done, we should (topically) delete it and rewrite it; rewriting will be much faster and we will rewrite with many lessons learned from the first attempt.

### How to create a good design?

- To create good design, the first step is to let go of the ego.
- Care about solving the problem, not a specific implementation.
    - We are not attached to the solutions; we are attached to solving the problems of our hands.
- 2 kinds of people are dangerous to work.
    - Who can't follow the instructions?
    - Who follows the instructions?
- Take time to review and code.
    - Code review and discussion: learn from others, teach to others.

### How to evaluate the quality of design?

- KISS - **Keep it simple stupid**
    - Simple keeps you focused.
    - Simple is easier to understand.
    - Simple solves only real problems we know about.
    - Simple fail less.
    - Simple code communicates what it does clearly without exposing confusing/surprising details.
- Complexity
    - 2 types of complexity.
        - Inherent complexity - comes from the problem domain.
        - Accidental complexity - comes from our implementation, e.g. deciding to use multi-threading.
- Simple is not necessarily familiar
    - Simple means it is easier to understand.
    - Familiar means we’re used to it, so it’s easy for us, but it doesn’t mean it’s simple.

> A good design hides the inherent complexity and eliminates the accidental complexity.
- Think YAGNI - **You Aren't Gonna Need It**
    - When I should implement something new.
        - *ASK* How much do you know about the problem domain?
        - Cost of implementing
        ```
        NOW ---------------- LATER
        $N         >          $L  --- postpone
        $N         ==         $L  --- postpone
        $N         <          $L  -
                    How probable?
                        High - do it
                        low - postpone
        ```
    - Why implement later?
        - we might learn more about the domain/vision/design of the thing we’re implementing e.g. we might figure out what DB features we need as the requirements clarify so we implement prod DB at the end.
        - we might turn out to not need that thing. 
        - (Thoughts: we might do some other high-ROI activity instead).
    - Postpone != procrastinate (procrastination is not getting things done that should have been done).
    - Don’t finalize one component at a time when several components interconnect. Work on several at a time and integrate them as they go along.
    - Don't do something, until you find value in doing it.
    - Why we don’t postpone?
        * Because we’re scared that we won’t have time for testing.
        * We take decisions early to test them and we’re stuck with them.
        * With good testing, we can postpone certain decisions of implementations.
- **Cohesion & Coupling**
    - Cohesion is where a piece of code is narrow, focused, and does one thing well. If a code is cohesive, it has to change less frequency.
    - Coupling is the degree of connectivity.
        - The worst form of coupling is *Inheritance*.
        - How to remove dependency.
            - Get rid of it.
            - Make it loose instead of tight.
            - Depending on a class is tight coupling, and depending on an interface is loose coupling.
        - High Cohesion - less responsibility.
        - Low Coupling - low dependency.
        - __A good design is high cohesion and low coupling__.
- DRY - **Don't repeat yourself**
    - Don’t duplicate code & effort.
        - similar subsets of code in different places but doing the same thing.
    - Every piece of knowledge in a system should have a single unambiguous authoritative representation.
    - *dry* reduces the cost of development.
- **Single Responsibility Principle**
    - The idea behind the SRP is that every class, module, or function in a program should have one responsibility/purpose in a program.
    - Long methods are bad.
        - Hard to test, reuse, debug, remember.
        - Obscure business logic.
        - Leads to duplicate.
        - Many reasons to change.
        - Obsolete comment.
        - Can't be optimized by anyhow.
        - Low cohesion and high coupling.
    - How long is a long method?
        - The number of lines can't be counted.
    - SLAP - *Single Level of Abstraction Principle* dictates the way you should organize your code (functions to be specific) to keep it maintainable.
    - Don't comment what instead of comment why
        - If you need to comment on what, you need to refactor.
- **Open/Closed Principle**
    - Software module (class, function, component) should be open for extension and closed for modification.
        - Closed from modification: don’t change older code when adding new features.
        - Open for extension: still add new features through polymorphism, reflection, and loose coupling.
    - Abstraction and Polymorphism are the keys to making this happen.
    - 2 options to make an enhancement.
        - change existing code ✗
        - add a small new module ✓
- **Liskov Substitution Principle**
    - Liskov Substitution Principle (LSP) states that objects of a superclass should be replaceable with objects of its subclasses without breaking the application.
    - Inheritance should be used only for substitutability.
        - If an object of `B` can be used anywhere an object of `A` is used then use `inheritance`.
        - If an object of `B` needs to use an object of `A`, then use `composition/delegation`.
    - Inheritance demands more from a developer than composition does.
    - Services of the derived class should require no more and promise no less than the corresponding services of the base class.
    - The user of a base class should be able to use an instance of a derived class without knowing the difference.
- **Dependency Inversion Principle**
    - A class shouldn't depend on another class, they should both depend on abstraction (interface).
    - DI solves OPC often enough.
- **Interface Segregation Principle**
    - The interface segregation principle (ISP) states that no code should be forced to depend on methods it does not use.
    - Make smaller interfaces instead of giant ones.
