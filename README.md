# Games Engineer Portfolio
Hi! I'm Nick. I'm currently a student studying computer science at UCLA and building a career in games. In my free time I make my own games and some cool graphics projects. This is a small portfolio showcasing those projects. Enjoy!

Jump to a specific project with the links below:
- [Particle Engine Project](#particle-engine): A 3D partile simulation in C++ and Raylib. Implementing custom spacial partitioning algorithms (octree, sweep and prune) for efficient collision detection
- [Godot Wild Jam #93](#godot-wild-jam93): A visual novel game built in a team of 5 with Godot. I implemented a custom dialog engine to import story text files written in Twine (a story-writing tool)
- [Trials of Yarbil](#toy): A top-down action game developed without an engine in Odin (a C-like language) and Raylib. This was a solo project where I built core engine systems like pathfinding, game serialization, level editors, and entity


<h2 id="particle-engine">Particle Engine Project</h2>

[Source Code](http://github.com/0megq/particle-engine) | C++, Raylib, CMake, Physics Simulation

A C++ 3D Particle Engine built with Raylib that simulates spherical particles.

This project is my first foray into separating the __broad and narrow phase__ during collision detection. My goal is to create a performant particle engine that can simulate __thousands of spherical particles__, allowing user interaction, and later support constraints so I can implement chains and soft-bodies.

![Particle Engine Demo Gif Failed to Load](./res/particle-engine-demo.gif)

__Euler Integration vs. Verlet Integration__: Currently, particles are simulated using Verlet integration which is a method of integrating physical motion without storing velocity. Verlet integration is a more accurate method than the standard Euler integration because it uses a centered integration. Instead of using only the current frame's velocity, Verlet Integration indirectly uses the average velocity between the current and previous frame. In practice, storing the previous position instead of a velocity lets us perform Verlet integration.

Storing the previous position instead of the current velocity has additional benefits. Since Verlet integration derives the velocity from the previous and current positions, I can resolve a collision by simply moving particles into a valid spot and letting Verlet integration derive the new velocity. The bouncing of particles seen in the gif above are the result of this.

Choosing not to store velocity comes with some challenges though. First off, forcing a particle to have a certain velocity cannot be done directly (giving the particle an initial velocity). Second, Verlet integration assumes the current frame time is equal to the previous frame time (I've chosen to leave out why this is exactly, as it'd make this write-up too long). This means that I must run the particle engine at a fixed framerate. This is rather simple to implement using a counter that accumulates frame time and run a particle system update once it reaches a fixed update time.

__Octree and spacial partioning__: After implementing the basic particle simulation, I wanted to optimize the 

Next steps:
1. Optimize further
    - Profile octree vs non-octree performance
    - Implement sweep and prune and multithread collision detection
2. Add user interaction
    - Enable/disable spawning with a button press
    - Let the user move particles a force on all particles
<h2 id="godot-wild-jam93"> Godot Wild Jam #93 (Holstein Collection Inc.) </h2>
[Demo](https://0megq.itch.io/holstein-collection-inc) with [Source Code](https://github.com/0megq/wildjam-aug26): Holstein Collection Inc. is a visual novel where you play as a bull collecting debt from those who've defaulted on their electricity bills. Made for the Godot Wild Jam #96.

<h2 id="toy">Steam Game (Trials of Yarbil)</h2>
[Engine and Gameplay Programming Sample](https://github.com/0megq/trials-of-yarbil-odin): Released solo Steam game. Trials of Yarbil is a top-down roguelike made with a custom engine written in Odin.

Interested in the design? Check out one of my devlogs


<!-- 
# Other Projects

[Unity and C# Sample](https://github.com/0megq/BookClubGameJam2025): This is a 3D point-and-click adventure game solo-developed in one month for the Book Club Game Jam 2025 in Unity. I worked on rigging an external

[Compute Shaders and Pixel Simulation Sample](https://github.com/0megq/cs-club-jam/tree/master): Falling sand simulation farming game. Written in Godot, it originally used GPU compute shaders, but proved too complex when integrating user interaction. The final version uses CPU simulation. -->
