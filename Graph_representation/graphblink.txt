import networkx as nx
import matplotlib.pyplot as plt
import time
from collections import deque
import heapq

def create_graph():
    """Creates a graph based on user input."""
    G = nx.Graph()
    n = int(input("Enter number of edges: "))
    print("Enter edges (format: node1 node2): ")
    for _ in range(n):
        u, v = input().split()
        G.add_edge(u, v)
    return G
def animate_traversal(graph, traversal_order, color, title):
    """Animates traversal step-by-step with the algorithm name as the figure title."""
    pos = nx.spring_layout(graph)  # Position nodes for visualization

    plt.figure(figsize=(8, 6))
    plt.suptitle(title, fontsize=14, fontweight='bold')  # Set figure title (algorithm name)
    
    nx.draw(graph, pos, with_labels=True, node_color='lightgray', edge_color='gray', node_size=2000, font_size=10)

    for i in range(len(traversal_order)):
        node = traversal_order[i]

        # Highlight traversed nodes
        plt.clf()
        plt.suptitle(title, fontsize=14, fontweight='bold')  # Ensure the figure title remains
        nx.draw(graph, pos, with_labels=True, node_color='lightgray', edge_color='gray', node_size=2000, font_size=10)
        nx.draw_networkx_nodes(graph, pos, nodelist=traversal_order[:i+1], node_color=color, node_size=2000)

        plt.title(f"Step {i+1}/{len(traversal_order)} - Visiting {node}")
        plt.pause(0.7)  # Pause to simulate animation

    plt.show()

def bfs(graph, start):
    """Performs BFS and returns the traversal order."""
    visited = set()
    queue = deque([start])
    bfs_order = []

    while queue:
        node = queue.popleft()
        if node not in visited:
            visited.add(node)
            bfs_order.append(node)
            queue.extend(neighbor for neighbor in graph.neighbors(node) if neighbor not in visited)

    return bfs_order

def dfs(graph, start, visited=None, dfs_order=None):
    """Performs DFS and returns the traversal order."""
    if visited is None:
        visited = set()
    if dfs_order is None:
        dfs_order = []

    visited.add(start)
    dfs_order.append(start)

    for neighbor in graph.neighbors(start):
        if neighbor not in visited:
            dfs(graph, neighbor, visited, dfs_order)

    return dfs_order

def astar(graph, start, goal, heuristic):
    """Performs A* search and returns the shortest path."""
    open_list = []
    heapq.heappush(open_list, (0 + heuristic[start], start))  # (f_cost, node)
    g_cost = {start: 0}
    parent = {start: None}

    while open_list:
        _, current = heapq.heappop(open_list)

        # If we reach the goal, reconstruct the path
        if current == goal:
            path = []
            while current is not None:
                path.append(current)
                current = parent[current]
            return path[::-1]  # Reverse the path to get it from start to goal
        
        # Explore neighbors
        for neighbor in graph.neighbors(current):
            tentative_g_cost = g_cost[current] + 1  # Assuming uniform cost (each edge has cost 1)
            
            if neighbor not in g_cost or tentative_g_cost < g_cost[neighbor]:
                g_cost[neighbor] = tentative_g_cost
                f_cost = tentative_g_cost + heuristic[neighbor]
                heapq.heappush(open_list, (f_cost, neighbor))
                parent[neighbor] = current
    
    return None  # If no path is found

# Main function
if _name_ == "_main_":
    G = create_graph()
    start_node = input("Enter start node: ")
    goal_node = input("Enter goal node for A*: ")

    # Heuristic values (example)
    heuristic = {}
    for node in G.nodes():
        heuristic[node] = int(input(f"Enter heuristic for node {node}: "))

    # BFS Animation
    bfs_order = bfs(G, start_node)
    print("BFS Traversal Order:", bfs_order)
    animate_traversal(G, bfs_order, color='blue', title="BFS")

    # DFS Animation
    dfs_order = dfs(G, start_node)
    print("DFS Traversal Order:", dfs_order)
    animate_traversal(G, dfs_order, color='red', title="DFS")

    # A* Animation
    astar_path = astar(G, start_node, goal_node, heuristic)
    print("A* Path:", astar_path)
    if astar_path:
        animate_traversal(G, astar_path, color='green', title="A*")
