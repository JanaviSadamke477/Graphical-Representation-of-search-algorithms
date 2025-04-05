# Graphical-Representation-of-search-algorithms
We have created a graphical representation of search algorithms like BFS, DFS & A* algorithm using NetworkX and Pygame.

---

# 🔍 Visualization Projects in Python

This repository contains two interactive visualization tools using `pygame`:

1. **Maze Pathfinding Visualizer**  
2. **Graph Blink Visualization**

---

## 1️⃣ Maze Pathfinding Visualizer

📖 **Overview**
This project is an interactive maze-solving visualizer built using Pygame. It supports three pathfinding algorithms:

1. Breadth-First Search (BFS)
2. Depth-First Search (DFS)
3. A* (A-Star)

Users can generate a new maze, set a start and end point, and watch the selected algorithm find a path in real-time.

### 📁 File: `mazepathfinding.py`

### 🔧 Requirements

Install the following:

```bash
pip install pygame
```

### 🚀 How to Run

```bash
python mazepathfinding.py
```

### 🧰 Dependencies
1. pygame
2. random
3. heapq
4. collections.deque

⚙️ **How It Works** 🕹️
- A grid-based maze is randomly generated.
-  Click to set the Start and Goal points.
-   Use keyboard controls to choose the algorithm:
   1 for BFS
   2 for DFS
   3 for A*
   R to regenerate the maze
   
### 🎨 Colors

| Color  | Meaning        |
|--------|----------------|
| 🟩 Green | Start Point     |
| 🟥 Red   | Goal Point      |
| 🟦 Blue  | Final Path      |
| ⬜ White | Free Path       |
| ⬛ Black | Wall            |
| 🩶 Gray  | Visited Nodes   |

### 📌 Features
1. Real-time animation of the algorithm's progress.
2. Displays visited cells and final path.
3. Highlights algorithm used at the top of the window.

   
## 📸 Screenshots

                                              Interface
                
![Image](https://github.com/user-attachments/assets/b59b77b9-425c-4eb6-9dea-e89715d844ec)
 
                                             A* Algorithm Output
                   
![Image](https://github.com/user-attachments/assets/22f0fef1-bd56-4f9a-99ce-d8d574b7f470)

                                            Depth-First-Search(DFS) Output

![Image](https://github.com/user-attachments/assets/092b0e76-2b0b-44b0-9b1e-ba3a25afb9d1)

                                    Breadth-First-Search(BFS) Output
                
![Image](https://github.com/user-attachments/assets/1fcdc56b-df7f-4533-bebe-8f2c80ee2736)






---

## 2️⃣ Graph Blink Visualization

📖 **Overview**
GraphBlink is a command-line + visual tool that lets users input custom graphs and visualize:
1. Breadth-First Search (BFS)
2.  Depth-First Search(DFS)
3.  A* Search

Animations are displayed using matplotlib to show step-by-step traversal or shortest path.

### 📁 File: `graphblink.py`


### 🔧 Requirements

Same dependency:

```bash
pip install pygame
```

### 🚀 How to Run

```bash
python graphblink.py
```
🧰 **Dependencies**
1. networkx
2. matplotlib
3. heapq
4. collections.deque
5. time

⚙️ **How It Works**
- User inputs the number of edges and edge connections.
- Sets a start node (and a goal for A*).
- Enters heuristic values for nodes.
- Visualizes traversal steps for BFS, DFS, and A* separately.

### 📌 Features
1. Animated step-by-step traversal
2. Color-coded nodes per algorithm
3. Accepts user-defined graph structure and heuristics


## 📎 Notes

- Ensure you're using **Python 3.6+**
- Both visualizations use `pygame` for GUI
- Projects are beginner-friendly for understanding algorithms

## 📸 Screenshots

                                          Initial setup
![Image](https://github.com/user-attachments/assets/54f8d845-1b46-4ddd-9bc2-165752f50f6c)


                                          A* algorithm output
![Image](https://github.com/user-attachments/assets/0c813441-2e12-41b2-8d08-61fffe46a09c)

                                          Depth-First-Search(DFS) Output
![Image](https://github.com/user-attachments/assets/c814790c-7245-4bee-b073-326a86d4a6f9)

                                        Breadth-First-Search(BFS) Output
![Image](https://github.com/user-attachments/assets/82001b62-5298-4761-a127-c06a57aa9bbf)

               
## 🧑‍💻 Author

Maintained by:-
1. Janavi Sadmake
2. Samiksha Bhagat
3. Deep Sawarkar
4. Yuvraj Vaidya
5. Sarthak Bokey
