To maximize our FOV, use the existing data feed from the lidar. Prioritize exploring the quadrant that has the lowest amount of cones 

# First Move
as a first, the robot should always perform a 360 degree scan to populate the grid as much as we can from the initial position 

# Exploration Insentives
Determine the priority of each clump based on factors such as:

- **Proximity**: Clumps closer to the robot (R) are less costly to reach.
- **Size**: Larger clumps might reveal more unseen territory.
- **Potential Information Gain**: Consider the expected amount of new visible cells that would be revealed by exploring this clump.

# Global A* Path Planning
- **Heuristic Function:**
    
    - A* uses a heuristic function to estimate the cost to reach the goal from the current cell. For exploration, you can use:
        - **Manhattan distance** for simple grids (sum of the absolute differences in the x and y coordinates).
        - Custom heuristic functions that factor in **information gain** (e.g., maximizing new cells revealed).
- **Priority Queue (Open List):**
    
    - Use a priority queue (e.g., a min-heap) to store cells to be explored, prioritized by their estimated cost (`f(n) = g(n) + h(n)`, where `g(n)` is the cost to reach the cell and `h(n)` is the heuristic).

    ```python
    import heapq

def heuristic(a, b):
    # Manhattan distance heuristic
    return abs(a[0] - b[0]) + abs(a[1] - b[1])

def a_star(grid, start, goal):
    open_list = []
    heapq.heappush(open_list, (0, start))  # (priority, position)
    came_from = {}
    cost_so_far = {start: 0}

    while open_list:
        _, current = heapq.heappop(open_list)

        if current == goal:
            # Reconstruct and return the path
            path = []
            while current != start:
                path.append(current)
                current = came_from[current]
            path.append(start)
            return path[::-1]  # Reverse the path

        x, y = current
        # Possible movement directions (up, down, left, right)
        neighbors = [(x - 1, y), (x + 1, y), (x, y - 1), (x, y + 1)]
        for nx, ny in neighbors:
            if 0 <= nx < len(grid) and 0 <= ny < len(grid[0]) and grid[nx][ny] != 'C':  # Check boundaries and obstacles
                new_cost = cost_so_far[current] + 1  # Assume uniform movement cost
                if (nx, ny) not in cost_so_far or new_cost < cost_so_far[(nx, ny)]:
                    cost_so_far[(nx, ny)] = new_cost
                    priority = new_cost + heuristic((nx, ny), goal)
                    heapq.heappush(open_list, (priority, (nx, ny)))
                    came_from[(nx, ny)] = current

    return None  # No path found

# Example grid
grid = [
    ['-', '-', 'C', '-', '-', '-', '-'],
    ['-', 'C', '-', '-', '-', '-', '-'],
    ['-', 'C', '-', '-', '-', 'C', '-'],
    ['-', '-', '-', 'L', '-', 'C', '-'],
    ['R', '-', 'C', '-', '-', '-', '-'],
    ['-', '-', '-', '-', '-', '-', 'C'],
    ['-', '-', '-', '-', '-', '-', '-']
]

start = (4, 0)  # Robot starting position
goal = (0, 1)  # Example goal position

path = a_star(grid, start, goal)
if path:
    print("Path found:", path)
else:
    print("No path found")

```

# A* Variants To Consider 
[Anytime A*](https://en.wikipedia.org/wiki/Anytime_A)
[Theta*](https://en.wikipedia.org/wiki/Theta* "Theta*")