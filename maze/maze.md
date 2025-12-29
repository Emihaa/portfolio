# [Maze Generation in Python, September 2025](https://github.com/Emihaa/MazeAlgorithm)

## Assignment Context

My third mentor assignment was to design and implement a maze generation algorithm. The primary constraint was that the maze had to be built from cubes rather than lines, which pushed the solution toward a grid-based representation instead of a traditional line-drawn maze.

In addition to the core task, there were optional bonus objectives: ensuring that all areas of the maze were accessible and implementing a seed argument so that the same seed would always generate the same maze.

## Technology Choices

![image](assignment.png)

Before implementing the algorithm itself, I spent time deciding which language and tools to use. My previous project had been written in C#, and using C again felt unnecessary for this assignment. After discussing the options with my mentor, I chose Python, as it is commonly expected from technical artists and would strengthen my portfolio with another relevant example.

For visualization, my mentor initially suggested Python’s turtle module. While easy to learn, it did not feel like the right fit for this project. Instead, I chose to use Pygame, as its rendering and event-handling model felt closer to the MLX42 graphics library we had previously used in school projects.

Setting up Pygame on my Windows laptop turned out to be the most challenging part of the project. Installing the required environment and resolving dependency issues took considerable effort, and interpreting error messages was often non-trivial. In this phase, tools like ChatGPT were invaluable in helping me understand installation errors and move forward efficiently.


## Maze Representation and Core Algorithm

The maze is represented as a grid of cubes, each classified as a border, wall, or room. The algorithm begins by creating an initial grid layout and then randomly selecting wall cubes as candidates for removal.

For each selected wall, the algorithm evaluates whether removing it would correctly connect two separate rooms. Only walls that separate exactly two rooms are eligible for removal, ensuring that the maze remains fully connected without introducing unintended shortcuts or loops.

This logic closely follows the principles behind Kruskal-style maze generation, adapted to a cube-based grid representation rather than line segments.
      
 ![images](Blender-screenshot.png)


## Flood Fill for Connectivity Validation

To determine whether two rooms are already connected, I implemented a flood fill algorithm. Starting from a given room, the flood fill recursively explores neighboring cubes in the north, east, south, and west directions, collecting all reachable rooms into a list.

When evaluating a wall, the algorithm performs flood fills on both sides of the wall and compares the resulting room lists. If the lists share common rooms, the areas are already connected, and the wall must not be removed. If the wall separates exactly two unconnected rooms, it can safely be removed.

While the logic itself was straightforward, this part of the implementation highlighted opportunities for a cleaner structure. The code worked correctly but was more verbose than necessary, and in hindsight could have been refactored into a more compact and reusable form.

## Visualization and Interaction

Rather than generating the maze instantly, I wanted the creation process to be visible in real time. Using Pygame’s event system, I implemented an animated generation loop that visualizes the maze as it is being built.

To improve usability and experimentation, I also added basic keyboard controls that allow the user to pause and reset the generation, adjust the animation speed, and change the seed value during runtime. Although Pygame’s event handling can feel somewhat cumbersome, it provides enough flexibility to support these interactive features.

## Bonus Features

Implementing a deterministic seed was straightforward using Python’s built-in random module. By initializing the random generator with a fixed seed value, the algorithm always selects cubes in the same order, producing identical maze layouts for the same seed.

The second bonus objective — ensuring that all maze areas are accessible — is effectively guaranteed by the algorithm itself. Since walls are only removed when they connect exactly two previously unconnected rooms, the resulting maze is always fully traversable.

## Code Structure and Lessons Learned

One of the most important lessons from this project was related to code organization. Many Pygame tutorials rely heavily on global variables, and by following that structure early on, I made later refactoring significantly more difficult.

Ideally, the project should have been built around a dedicated class encapsulating the maze state and its behavior. Due to time constraints, I chose to complete the project using the existing structure, fully aware that the code was functional but not as clean or modular as it could be.

Based on this experience, my mentor recommended further reading on clean code practices, an insight I fully agree with and plan to apply in future projects.

## Extending the Project: Pathfinding

After completing the maze generator, the project proved useful beyond its original scope. In a school-organized challenge where teams competed by writing AI for a turn-based strategy game, I volunteered to implement the pathfinding and scouting logic.

I extended this project by adding entrance and exit points to the maze and implemented a breadth-first search algorithm to find the shortest path between them. Since there is only one exit, the algorithm can terminate early as soon as the exit is found, returning the shortest path or null if no path exists.

This implementation served as a practical stepping stone before implementing similar pathfinding logic in Go for the competition project.

## Conclusion

Overall, this project achieved its goals successfully. It resulted in a functional and visually clear maze generator while providing valuable experience in algorithm design, grid-based logic, visualization, and real-time interaction.

While the current codebase would benefit from a full rewrite to improve structure and cleanliness, the project itself stands as a strong portfolio example. It also influenced my approach to future work by reinforcing the importance of planning code structure earlier, especially when following tutorials. I plan to revisit and refine this project in the future, applying the lessons learned to create a cleaner and more maintainable implementation.


---------------------------------------------------------------------------------------------------------------------------------------------------------------
---------------------------------------------------------------------------------------------------------------------------------------------------------------
