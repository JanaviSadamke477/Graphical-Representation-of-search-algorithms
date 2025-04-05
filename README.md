# Graphical-Representation-of-search-algorithms
We have created a graphical representation of search algorithms like BFS, DFS &amp; A* algorithm using NetworkX and Pygame.
Sure! Here's the full content of the `README.md` file I created for you:

---

# 🔍 Visualization Projects in Python

This repository contains two interactive visualization tools using `pygame`:

1. **Maze Pathfinding Visualizer**  
2. **Graph Blink Visualization**

---

## 1️⃣ Maze Pathfinding Visualizer

A visual simulation of pathfinding algorithms in a randomly generated maze. Users can set start and end points and watch how BFS, DFS, and A* search solve the maze.

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

### 🕹️ Controls

- Press `1` — BFS  
- Press `2` — DFS  
- Press `3` — A*  
- Press `R` — Regenerate maze  
- **Mouse Left Click (twice)** — Set Start and Goal points

### 🎨 Colors

| Color  | Meaning        |
|--------|----------------|
| 🟩 Green | Start Point     |
| 🟥 Red   | Goal Point      |
| 🟦 Blue  | Final Path      |
| ⬜ White | Free Path       |
| ⬛ Black | Wall            |
| 🩶 Gray  | Visited Nodes   |

## 📸 Screenshots

                                          Initial setup
![Image](https://github.com/user-attachments/assets/54f8d845-1b46-4ddd-9bc2-165752f50f6c)


                                          A* algorithm output
![Image](https://github.com/user-attachments/assets/0c813441-2e12-41b2-8d08-61fffe46a09c)

                                          Depth-First-Search(DFS) Output
![Image](https://github.com/user-attachments/assets/c814790c-7245-4bee-b073-326a86d4a6f9)

                                        Breadth-First-Search(BFS) Output
![Image](https://github.com/user-attachments/assets/82001b62-5298-4761-a127-c06a57aa9bbf)

---

## 2️⃣ Graph Blink Visualization

`graphblink.py` (Assumed functionality: visualizing nodes/edges blinking for some animation purpose).

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

### 📌 Description

This file visually represents graph nodes and connections in an animated fashion. It may be used to show graph transitions, highlights, or algorithm steps.

## 📎 Notes

- Ensure you're using **Python 3.6+**
- Both visualizations use `pygame` for GUI
- Projects are beginner-friendly for understanding algorithms

## 📸 Screenshots


## 🧑‍💻 Author

Maintained by:-
1. Janavi Sadmake
2. Samiksha Bhagat
3. Deep Sawarkar
4. Yuvraj Vaidya
5. Sarthak Bokey
