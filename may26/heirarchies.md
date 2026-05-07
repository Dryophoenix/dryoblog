# Hierarchies

## DryoX

  DryoX is my own codebase, made in such a way that anyone can use it. It is primarily written in C, with some POSIX sh written as well, so you can communicate with it.

  It's also *hierarchical*. 

  I believe there's a valuable way to reduce bloat in larger codebases, and my way of addressing the problem is establishing a strong hierarchy.

### Core Library the Matriarch

  At the heart of my codebase is `libdryox`. This is where many of my really, truly basic functions live. This includes logging functions. This includes a TOML parser. In general, this includes all the functions that its children rely on.

  If a function exists in two of its "children", it must be promoted to "parent". This has four categories, and I rely on the Eisenhower Matrix method of triaging these.

  1) Does the function have the exact same purpose as one of its "siblings"? 

    If so, it should probably be promoted to their parent.
    This would be prioritized as Eisenhower 1 - Urgent and Important.

  2) Does the function have the exact same purpose as one of its "cousins"?
    
    If so, it should probably be promoted to the closest parent match.
    This would be prioritized as Eisenhower 3 - Not Urgent and Important.

  3) Does the function have a purpose that's similar to a "sibling's" function, but could reasonably stay separate?

    If so, it should eventually be promoted to their parent. This would actually be prioritized as Eisenhower 4, not urgent and unimportant. 

  4) Does the function have a purpose that's similar to a "cousin's" function, but could reasonably stay separate?

    If so, it should be eventually promoted to the closest parent match. This would also be prioritized as Eisenhower 4 - Not urgent and unimportant.

  Using the Eisenhower matrix model allows for effective triaging of *maintenance* in this case, which otherwise can be difficult. Especially because of the nature of programming, Eisenhower 4 tasks don't have to be discarded- I would presume that they make excellent introductory projects to a codebase, since they require only a reimplementation of the code, and would provide opportunity for new contributors to enter. I've noticed that many codebases - especially distributions of Linux - have "good for new contributors" pages in their triage system. This also just serves as a valid way to fill that, without filling experienced contributors' to-do lists with tasks.

  Granted, for my small codebase, this hardly matters. If more programmers start to adopt it, though, maybe someone will take an interest, and they can learn the code by reimplementing it. 

  I'm not entirely sure when exactly I determined my code would be structured this way, but I do remember why.

### Application Library the Child
  
  In the process of building a library called `dryoconnect`, which is an SSH tool built on `libdryox`, I determined that it could be considered a "child" of DryoX. 

  My primitive Bash version of the tool found itself with a predicament - it was writing a lot of logging functions, and it was building its own config parser out of a Bash associative array. Figuring that this was beginning to become unwieldy, I began to learn C.

  In the process of hashing out how I wanted the project to be structured, I knew that the logging functions would have to live in `libdryox`, `dryoconnect`'s parent. I also asked, "how exactly should functions that are this ubiquitous be treated from now on?"

  And from that, I have built my libraries hierarchically.

\- Dryophoenix (Neph Hillis)

dryophoenix@outlook.com
