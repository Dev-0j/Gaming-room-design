# Gaming-room-design
Software design document for The Gaming Room's Draw It or Lose It web port. Covers singleton and iterator pattern implementation, domain model, and platform/architecture recommendations for CS-230.

# Gaming-room-design

Software design document for The Gaming Room's Draw It or Lose It web port. Covers singleton and iterator pattern implementation, domain model, and platform/architecture recommendations for CS-230.

## Module 8 Journal Reflection

**1. Briefly summarize The Gaming Room client and their software requirements. Who was the client? What type of software did they want you to design?**

The client was The Gaming Room, looking to take their game Draw It or Lose It from an Android-only app to a web-based version that works across desktop, mobile, and tablet. The core requirements were: only one instance of the game service can exist in memory at a time, game/team/player names have to be unique within their scope, and every game/team/player needs a unique ID and name. I addressed these with a singleton GameService, the iterator pattern for uniqueness checks, and an Entity base class for shared ID/name behavior.

**2. What did you do particularly well in developing this documentation?**

I think the strongest part was connecting every design decision directly back to a specific client requirement instead of just describing patterns in the abstract. For example, I didn't just say I used the singleton pattern, I tied it to the exact requirement (only one game instance in memory) and explained what would break without it. Same with the platform evaluation table, I didn't just rate each OS, I reasoned through cost, licensing, and how it interacts with the others, like why mobile can't be a server host but is the hardest client to support.

**3. What about the process of working through a design document did you find helpful when developing the code?**

Writing the design constraints section before touching code forced me to think through problems I would've otherwise hit mid-implementation, like the fact that a singleton in a single JVM doesn't actually guarantee one instance once you're running multiple server processes. Working through the domain model relationships (composition vs. association) up front also made the actual class structure obvious before I wrote a line of Java, since the design doc already specified that Game owns Teams and Team owns Players.

**4. If you could choose one part of your work on these documents to revise, what would you pick? How would you improve it?**

I'd revise the Distributed Systems and Networks section. I covered the client-server model and WebSockets at a high level, but I'd add more detail on failure handling, specifically what happens to the other players in a game if one player's connection drops mid-round, since I mention it needs to be handled gracefully but don't specify how.

**5. How did you interpret the user's needs and implement them into your software design? Why is it so important to consider the user's needs when designing?**

The client's needs weren't just feature requests, they were constraints that shaped the architecture. Only one game instance became a singleton. Unique names became a coordinated lookup using the iterator pattern. Considering user needs matters because a design that satisfies requirements on paper but ignores how they'll actually be used in production, like the uniqueness check not accounting for concurrent requests, would pass a code review but fail in real use.

**6. How did you approach designing software? What techniques or strategies would you use in the future to analyze and design a similar application?**

I started from the client's stated requirements, then worked backward to the design patterns and class structure that would satisfy them, rather than picking patterns first and looking for a use. In the future I'd keep using that requirement-to-pattern mapping, and earlier in the process I'd also map out constraints (network, concurrency, security) before finalizing the domain model, since some of those constraints affect class design decisions, not just deployment.
