---
layout: essay
type: essay
title: "Blueprints, Not Crutches: How Design Patterns Shape Software Engineering"
date: 2025-04-25
published: true
labels:
  - software engineering
  - design patterns
  - development
---

# Blueprints, Not Crutches: How Design Patterns Shape Software Engineering

When I first started building websites with Next.js and React, I thought I was just assembling and reusing parts — throwing in a Bootstrap navbar here, wiring up a form with state hooks there. It felt improvisational, like solving problems by instinct, not by plan.  
Later, I realized that much of what I was doing unknowingly followed well-established paths. I had stumbled onto something deeper: design patterns. These aren't rigid rules or plug-and-play kits. Design patterns are time-tested ways of solving common software challenges. They’re solutions to the same problems we have to face again and again, offering structured approaches without taking away creativity.

## Seeing the Patterns in My Own Projects

The moment I understood design patterns, I saw them everywhere in my work — especially in our current group project, Manoa’s Got Music.  
When we needed our app to display different interfaces — the landing page, browse musicians, jam sessions, user profile — based on user actions, we unconsciously built around the State Pattern. We maintain a single view variable that determines the current screen, making transitions predictable and centralized.  
When setting up our login and registration system, we applied ideas from the Factory Pattern. New users are created based on their role (USER or ADMIN), with appropriate fields and permissions initialized based on the account type.

Here’s a simplified example of how a Factory Pattern looks in practice:

```javascript
function createUser(role) {
  if (role === "ADMIN") {
    return { role: "ADMIN", permissions: ["manage_users", "edit_content"] };
  } else {
    return { role: "USER", permissions: ["view_content"] };
  }
}

// Usage
const admin = createUser("ADMIN");
const user = createUser("USER");
```


Even our Navbar behavior, dynamically highlighting the active page and adapting based on login status, mirrors the Strategy Pattern: different behaviors triggered based on the user's current state.  
These patterns helped us structure the project cleanly, even while working locally without a deployed backend. They gave us the flexibility to add features like an Edit Profile page, Jam Session scheduling, and eventually an Admin Dashboard without rewriting core logic.

## Patterns Aren't Shortcuts — They're Roadmaps

Early on, I thought design patterns would restrict creativity. Now, I understand they amplify it. Patterns don't eliminate problem-solving — they focus on it. A big part of software engineering today is finding optimal solutions that already exist and adapting these design patterns. As software engineers, we often face similar problems repeatedly.  
Design patterns give us a shared language to tackle these challenges faster and more thoughtfully. Instead of starting from scratch every time, we can recognize what kind of problem we’re facing and reach for a solution that has been proven to work, while still shaping it to fit our unique needs.  
Learning to see patterns isn’t about memorizing definitions; it’s about building instincts for good design. The more I work with them, the more I realize that mastering design patterns isn’t the end goal, it’s just the beginning of writing better, smarter software.
