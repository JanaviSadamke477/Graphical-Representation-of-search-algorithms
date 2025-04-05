import pygame
import random
import heapq
from collections import deque

# Constants
WIDTH, HEIGHT = 750, 750
ROWS, COLS = 32,32  # Default Grid size
CELL_SIZE = WIDTH // COLS
WHITE, BLACK, GREEN, BLUE, RED, GRAY, YELLOW = (255, 255, 255), (0, 0, 0), (0, 255, 0), (0, 0, 255), (255, 0, 0), (200, 200, 200), (0, 255, 250)

# Initialize Pygame
pygame.init()
screen = pygame.display.set_mode((WIDTH, HEIGHT))
CELL_SIZE = WIDTH // COLS  # Recalculate the cell size based on the new screen width
pygame.display.set_caption("Maze Solving Visualization")
clock = pygame.time.Clock()

# Initialize font for algorithm name display
font = pygame.font.SysFont('Arial', 30)

# Generate Maze (Random)
def generate_maze():
    grid = [[1 if random.random() > 0.3 else 0 for _ in range(COLS)] for _ in range(ROWS)]
    return grid

# Draw the Grid
def draw_grid(grid, start, goal, path=None, visited=None, algorithm_name=""):
    screen.fill(WHITE)
    for r in range(ROWS):
        for c in range(COLS):
            color = WHITE if grid[r][c] else BLACK
            pygame.draw.rect(screen, color, (c * CELL_SIZE, r * CELL_SIZE, CELL_SIZE - 1, CELL_SIZE - 1))

    if visited:
        for r, c in visited:
            pygame.draw.rect(screen, GRAY, (c * CELL_SIZE, r * CELL_SIZE, CELL_SIZE - 1, CELL_SIZE - 1))

    if path:
        for r, c in path:
            pygame.draw.rect(screen, BLUE, (c * CELL_SIZE, r * CELL_SIZE, CELL_SIZE - 1, CELL_SIZE - 1))

    if start:
        pygame.draw.rect(screen, GREEN, (start[1] * CELL_SIZE, start[0] * CELL_SIZE, CELL_SIZE - 1, CELL_SIZE - 1))

    if goal:
        pygame.draw.rect(screen, RED, (goal[1] * CELL_SIZE, goal[0] * CELL_SIZE, CELL_SIZE - 1, CELL_SIZE - 1))
# Display the algorithm name at the top of the screen
    algorithm_text = font.render(f"Algorithm: {algorithm_name}", True, YELLOW)
    screen.blit(algorithm_text, (10, 10))  # You can adjust the (10, 10) position as needed

    pygame.display.flip()
   

# BFS Algorithm (with real-time steps)
def bfs(grid, start, goal):
    queue = deque([start])
    came_from = {start: None}
    visited = set([start])
    steps = []

    while queue:
        node = queue.popleft()
        steps.append(node)  # Track the steps taken so far
        if node == goal:
            return reconstruct_path(came_from, goal), visited, steps
        for neighbor in get_neighbors(grid, node):
            if neighbor not in visited:
                queue.append(neighbor)
                visited.add(neighbor)
                came_from[neighbor] = node

    return [], visited, steps

# DFS Algorithm (with real-time steps)
def dfs(grid, start, goal):
    stack = [start]
    came_from = {start: None}
    visited = set([start])
    steps = []

    while stack:
        node = stack.pop()
        steps.append(node)  # Track the steps taken so far
        if node == goal:
            return reconstruct_path(came_from, goal), visited, steps
        for neighbor in get_neighbors(grid, node):
            if neighbor not in visited:
                stack.append(neighbor)
                visited.add(neighbor)
                came_from[neighbor] = node

    return [], visited, steps

# A* Algorithm (with real-time steps)
def astar(grid, start, goal):
    open_set = []
    heapq.heappush(open_set, (0, start))
    g_cost = {start: 0}
    came_from = {start: None}
    visited = set()
    steps = []

    while open_set:
        _, current = heapq.heappop(open_set)
        visited.add(current)
        steps.append(current)  # Track the steps taken so far
        if current == goal:
            return reconstruct_path(came_from, goal), visited, steps

        for neighbor in get_neighbors(grid, current):
            new_g_cost = g_cost[current] + 1
            if neighbor not in g_cost or new_g_cost < g_cost[neighbor]:
                g_cost[neighbor] = new_g_cost
                f_cost = new_g_cost + heuristic(neighbor, goal)
                heapq.heappush(open_set, (f_cost, neighbor))
                came_from[neighbor] = current

    return [], visited, steps

# Get Neighbors for Pathfinding
def get_neighbors(grid, node):
    r, c = node
    neighbors = []
    for dr, dc in [(0, 1), (1, 0), (0, -1), (-1, 0)]:
        nr, nc = r + dr, c + dc
        if 0 <= nr < ROWS and 0 <= nc < COLS and grid[nr][nc] == 1:
            neighbors.append((nr, nc))
    return neighbors

# Reconstruct Path
def reconstruct_path(came_from, goal):
    path = []
    node = goal
    while node:
        path.append(node)
        node = came_from[node]
    return path[::-1]

# Heuristic for A*
def heuristic(a, b):
    return abs(a[0] - b[0]) + abs(a[1] - b[1])

# Main Loop
def main():
    grid = generate_maze()
    start, goal = None, None
    running = True
    algorithm = "BFS"
    path, visited, steps = [], set(), []

    while running:
        draw_grid(grid, start, goal, path, visited, algorithm_name=algorithm)

        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                running = False

            if event.type == pygame.KEYDOWN:
                if event.key == pygame.K_1:
                    algorithm = "BFS"
                elif event.key == pygame.K_2:
                    algorithm = "DFS"
                elif event.key == pygame.K_3:
                    algorithm = "A*"
                elif event.key == pygame.K_r:
                    grid = generate_maze()
                    start, goal = None, None
                    path, visited, steps = [], set(), []

            if event.type == pygame.MOUSEBUTTONDOWN:
                x, y = pygame.mouse.get_pos()
                row, col = y // CELL_SIZE, x // CELL_SIZE
                if not start:
                    start = (row, col)
                elif not goal:
                    goal = (row, col)

                if start and goal:
                    if algorithm == "BFS":
                        path, visited, steps = bfs(grid, start, goal)
                    elif algorithm == "DFS":
                        path, visited, steps = dfs(grid, start, goal)
                    elif algorithm == "A*":
                        path, visited, steps = astar(grid, start, goal)

                    # Visualize the steps taken by the algorithm
                    for step in steps:
                        draw_grid(grid, start, goal, path, visited, algorithm_name=algorithm)
                        pygame.draw.rect(screen, BLUE, (step[1] * CELL_SIZE, step[0] * CELL_SIZE, CELL_SIZE - 1, CELL_SIZE - 1))
                        pygame.display.flip()
                        pygame.time.delay(100)  # Slow down the visualization for better effect

                    pygame.time.delay(100)  # Wait a moment after showing all steps

    pygame.quit()

if _name_ == "_main_":
    main()