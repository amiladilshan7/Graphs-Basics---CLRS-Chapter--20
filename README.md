# Graphs-Basics---CLRS-Chapter--20
This repository covers the fundamental concepts of graphs from Chapter 20 of Introduction to Algorithms (CLRS). It includes clear explanations and Python code templates to help you understand and implement essential graph algorithms and data structures.


## 📂 What’s Inside This Repo?

* 🔹 Python templates for graph data structures
* 🔹 Implementations of graph representations
* 🔹 Learning-friendly comments and quizzes

---

# 📘 CLRS Chapter 20 – Graph Basics with Python

Welcome to this repository! It covers the **fundamentals of graphs** based on **Chapter 20 of *Introduction to Algorithms* (CLRS)**, with Python code templates to help you grasp key concepts and implement them easily.

---

## 📍 What Is a Graph?

**Simple Definition:**
A graph is a way to **model relationships** between objects.

It consists of:

* **Vertices (nodes):** The objects (e.g., people, cities, webpages)
* **Edges (connections):** The links or paths between them

---

## 📦 Real-Life Examples

| Graph Concept   | Real-Life Example                 |
| --------------- | --------------------------------- |
| Vertices        | Cities                            |
| Edges           | Roads between cities              |
| Weights         | Distance or travel cost           |
| Directed Edge   | One-way street                    |
| Undirected Edge | Two-way road or mutual friendship |

---

## 🧠 Why Learn Graphs? 

Graphs help solve many real-world problems like:

* 📍 **Shortest Path** → Google Maps
* 🧑‍🤝‍🧑 **Social Networks** → Mutual friends
* 🌐 **Network Routing** → Internet data flow
* 📦 **Dependency Trees** → Package managers, build systems
* 🧭 Maze solving, project planning, recommendations, and more!

**🔑 Mastering graphs = solving complex problems efficiently.**

---

## ✏️ Graph Terminology (Core 20%)

| Term        | Meaning                                               |
| ----------- | ----------------------------------------------------- |
| Vertex (v)  | A node in the graph                                   |
| Edge (u, v) | A connection/link from node `u` to node `v`           |
| Adjacency   | Two nodes are adjacent if they are directly connected |
| Degree      | Number of edges connected to a node                   |
| Path        | Sequence of nodes connected by edges                  |
| Cycle       | A path that starts and ends at the same node          |
| Connected   | Every node is reachable from any other node           |

---

## 🧮 Graph Representations in Code

### 🥇 1. **Adjacency List** (Most Common ✅)

Use a dictionary or list to store the neighbors of each node.
**Space Efficient:** `O(V + E)`

```python
graph = {
    "A": ["B", "C"],
    "B": ["A", "D"],
    "C": ["A"],
    "D": ["B"]
}
```

### 🥈 2. **Adjacency Matrix**

Use a 2D array to represent connections.
**Good for dense graphs.**
**Space:** `O(V²)`

```python
#    A  B  C  D
# A [0, 1, 1, 0]
# B [1, 0, 0, 1]
# C [1, 0, 0, 0]
# D [0, 1, 0, 0]
```

---

## 🧩 Real-Life Analogy

* **Adjacency List** → Your phone's **Contacts app**
  Each person (node) has a list of contacts (neighbors).

* **Adjacency Matrix** → A **Friendship table**
  Rows and columns are people. If two are friends → 1; else → 0.

---

## 🧠 Quiz Time: Graph Basics

1. In a graph of cities, what does an edge represent?
2. Which representation is better for **sparse** graphs?
3. If you have **1000 vertices and only 10 edges**, which structure is more memory efficient?
4. What does it mean if a graph is **connected**?

<details>
  <summary>✅ Show Answers</summary>

1. A connection/road between two cities
2. Adjacency List
3. Adjacency List
4. Every vertex can be reached from any other vertex

</details>

---


---

## 🚶‍♂️ What is Graph Traversal?

### ✅ Definition:

Graph traversal means **visiting all the vertices** of a graph in a specific order, starting from a chosen node.

There are two major traversal strategies:

* **🔵 Breadth-First Search (BFS):** Explore layer by layer
* **🔴 Depth-First Search (DFS):** Explore deep before wide

---

## 🚍 Breadth-First Search (BFS)

### 🎯 Goal:

Explore the graph **level by level**, starting from the source node.

### 🔁 Real-Life Analogy:

Imagine you’re calling friends to spread a message:

1. You first call your **immediate friends**.
2. They call **their friends**.
3. The wave continues outward...

📌 **This is BFS** — it spreads out in layers, like waves 🌊.

---

### 📜 BFS Pseudocode (CLRS-style):

```text
BFS(G, s):
  for each vertex v in G:
    v.color = WHITE
    v.distance = ∞
    v.parent = NIL

  s.color = GRAY
  s.distance = 0
  s.parent = NIL

  Q = empty queue
  ENQUEUE(Q, s)

  while Q is not empty:
    u = DEQUEUE(Q)
    for each v in Adj[u]:
      if v.color == WHITE:
        v.color = GRAY
        v.distance = u.distance + 1
        v.parent = u
        ENQUEUE(Q, v)
    u.color = BLACK
```

---

### 🧑‍💻 Python Code Example

```python
from collections import deque

def bfs(graph, start):
    visited = set()
    queue = deque([start])
    
    while queue:
        node = queue.popleft()
        if node not in visited:
            print(node)
            visited.add(node)
            queue.extend(neighbor for neighbor in graph[node] if neighbor not in visited)
```

---

### 🌳 Example Graph (Adjacency List)

```python
graph = {
    'A': ['B', 'C'],
    'B': ['D', 'E'],
    'C': ['F'],
    'D': [],
    'E': ['F'],
    'F': []
}
```

**BFS starting at 'A' → Output:**

```
A
B
C
D
E
F
```

---


---

## 🕳️ What is Depth-First Search (DFS)?

### ✅ Definition:

DFS (Depth-First Search) explores **as far as possible along one path** before backtracking to explore alternative branches.

---

### 🔁 Real-Life Analogy:

Imagine you're exploring a maze:

* At every turn, you **go deep** down one path.
* If you hit a dead end, you **backtrack** to the last decision point and try a different path.

That’s exactly how DFS works!

---

### 📜 DFS Pseudocode (CLRS-Style, Recursive)

```text
DFS(G)
  for each vertex u in G:
    u.color = WHITE
    u.parent = NIL
  time = 0
  for each vertex u in G:
    if u.color == WHITE:
      DFS-VISIT(G, u)

DFS-VISIT(G, u)
  time = time + 1
  u.d = time
  u.color = GRAY
  for each v in Adj[u]:
    if v.color == WHITE:
      v.parent = u
      DFS-VISIT(G, v)
  u.color = BLACK
  time = time + 1
  u.f = time
```

---

### 🧑‍💻 Python Code Example (Recursive)

```python
def dfs(graph, start, visited=None):
    if visited is None:
        visited = set()
    visited.add(start)
    print(start)
    for neighbor in graph[start]:
        if neighbor not in visited:
            dfs(graph, neighbor, visited)
```

---

### 🧪 Example Graph (Adjacency List)

```python
graph = {
    'A': ['B', 'C'],
    'B': ['D', 'E'],
    'C': ['F'],
    'D': [],
    'E': ['F'],
    'F': []
}
```

### ▶️ DFS Traversal Starting from 'A':

```
A B D E F C
```

> ⚠️ **Note:** DFS output may vary depending on the **order of neighbors** in the graph.

---


---

## 🚀 What Is Topological Sorting?

A **topological sort** of a **Directed Acyclic Graph (DAG)** is a **linear ordering of its vertices** such that for every directed edge `u → v`, vertex `u` comes **before** `v` in the ordering.

---

### 📅 Real-Life Analogy: **Task Scheduling**

Imagine you're preparing a meal. Some steps must happen **before** others:

* ✅ Chop veggies **before** cooking them
* ✅ Preheat oven **before** baking the cake
* ✅ Set the table **after** finishing cooking

These are **dependencies**, and a **topological sort** gives you a valid sequence that respects all such constraints.

---

### 🔹 Key Requirements

| Condition      | Must Be True            |
| -------------- | ----------------------- |
| Graph Type     | **Directed**            |
| Cycle Presence | **No Cycles (Acyclic)** |

> ❗ You **cannot** topologically sort a graph with cycles (like A → B → A).

---

## ✅ Topological Sort Algorithms

---

### A. **Kahn's Algorithm** (BFS-Style)

**Steps:**

1. Compute in-degree (incoming edges) for each node
2. Start with nodes having **in-degree = 0**
3. Repeatedly:

   * Remove a node from the queue
   * Add it to the result
   * Reduce in-degree of its neighbors
   * Add neighbors to the queue if their in-degree becomes 0
4. If all nodes are processed → success
   Else → the graph has a cycle ❌

#### 🧑‍💻 Python Code – Kahn’s Algorithm

```python
from collections import deque, defaultdict

def topo_sort_kahn(nodes, edges):
    in_deg = {u: 0 for u in nodes}
    adj = defaultdict(list)
    
    for u, v in edges:
        adj[u].append(v)
        in_deg[v] += 1

    q = deque([u for u in nodes if in_deg[u] == 0])
    topo = []

    while q:
        u = q.popleft()
        topo.append(u)
        for v in adj[u]:
            in_deg[v] -= 1
            if in_deg[v] == 0:
                q.append(v)

    if len(topo) != len(nodes):
        raise ValueError("Graph has a cycle!")
    return topo
```

---

### B. **DFS-Based Topological Sort**

**Steps:**

1. Perform **DFS** on unvisited nodes
2. After visiting all neighbors of a node, **push it onto a stack**
3. Finally, **reverse** the stack to get the topological order

#### 🧑‍💻 Python Code – DFS Approach

```python
def dfs_topo(nodes, adj):
    visited = set()
    topo = []

    def dfs(u):
        visited.add(u)
        for v in adj[u]:
            if v not in visited:
                dfs(v)
        topo.append(u)

    for u in nodes:
        if u not in visited:
            dfs(u)

    topo.reverse()
    return topo
```

---

## 🧠 Flashcards for Quick Review

| Term / Concept            | Flashcard                                                  |
| ------------------------- | ---------------------------------------------------------- |
| What is Topological Sort? | Ordering of vertices so that all directed edges go `u → v` |
| Required Graph Type       | **DAG** (Directed Acyclic Graph)                           |
| Kahn’s Algorithm Uses     | **BFS + in-degree counting**                               |
| DFS-Based Approach Uses   | **Post-order DFS + reverse output**                        |
| Time Complexity           | `O(V + E)`                                                 |
| Real-Life Analogy         | **Scheduling tasks with dependencies**                     |

---

## 🧪 Quick Quiz on Topological Sort

1. What kind of graph can be topologically sorted?
2. Why can’t you sort a graph with a cycle?
3. Which algorithm uses in-degrees and a queue?
4. Which method reverses post-order of DFS?
5. What’s the time complexity?


---

---

## 📘 What Is a Strongly Connected Component (SCC)?

In a **directed graph**, a **Strongly Connected Component (SCC)** is a **maximal group of vertices** where:

> For **every pair of nodes** `u` and `v` in the group,
> you can reach `v` from `u` **and** reach `u` from `v`.

---

### 🧠 Simply Put:

Inside an SCC, **everything is reachable from everything else** — no dead ends or one-way paths.

---

### 🎯 Real-World Analogy: **WhatsApp Group Chat**

* Everyone can message everyone else.
* Full, two-way communication.
* If someone **can message but not receive**, they’re **not part of the SCC**.

---

### 📍 Why Do SCCs Matter?

SCCs help us **understand structure** in directed graphs and are useful in:

* 🔗 **Web Crawling** → Detecting loops in links
* 📦 **Compilers** → Handling mutually dependent modules
* 🧑‍🤝‍🧑 **Social Networks** → Finding tightly-knit circles
* 🧠 **Control Flow** in code and circuits

---

## 🕸️ Example Graph and Its SCCs

```
A → B → C → A       (SCC 1)
D → E → F → D       (SCC 2)
G                  (SCC 3 - single node)
```

🔍 **Detected SCCs:**

* `{A, B, C}`
* `{D, E, F}`
* `{G}`

---

## 🔍 How to Find SCCs: **Kosaraju’s Algorithm (CLRS)**

Kosaraju’s algorithm uses **two DFS passes** to find SCCs.

---

### ✅ Step-by-Step Breakdown

1. **First DFS (Original Graph):**

   * Visit nodes and record **finishing times** (post-order).
   * Think of this as: "How deep can I go before backing out?"

2. **Reverse the Graph:**

   * Flip every edge: `u → v` becomes `v → u`.

3. **Second DFS (Reversed Graph):**

   * Run DFS in **decreasing order of finishing times**.
   * Each DFS tree in this pass forms **one SCC**.

---

### 📦 Why Does This Work?

Reversing the graph **turns SCC roots into entry points**.
Starting DFS from highest finishing time ensures **all SCCs are found without overlap**.

---

## 🧑‍💻 Python-Style Pseudocode

```python
def kosaraju_scc(graph):
    visited = set()
    finish_stack = []

    # Step 1: DFS to compute finishing times
    def dfs1(u):
        visited.add(u)
        for v in graph[u]:
            if v not in visited:
                dfs1(v)
        finish_stack.append(u)

    for node in graph:
        if node not in visited:
            dfs1(node)

    # Step 2: Reverse the graph
    reversed_graph = reverse_graph(graph)

    # Step 3: DFS on reversed graph
    visited.clear()
    sccs = []

    def dfs2(u, component):
        visited.add(u)
        component.append(u)
        for v in reversed_graph[u]:
            if v not in visited:
                dfs2(v, component)

    while finish_stack:
        node = finish_stack.pop()
        if node not in visited:
            component = []
            dfs2(node, component)
            sccs.append(component)

    return sccs
```

> 💡 *You’ll need to implement `reverse_graph(graph)` based on your graph format.*

---

## 🧠 Flashcards: Strongly Connected Components

| Concept                | Flashcard                                         |
| ---------------------- | ------------------------------------------------- |
| What is SCC?           | Group where every node can reach every other node |
| Required Graph Type    | **Directed Graph**                                |
| Key Algorithm          | **Kosaraju’s Algorithm**                          |
| First DFS Pass Does?   | Records finishing times                           |
| Second DFS Pass Does?  | Explores reversed graph in post-order             |
| Time Complexity        | `O(V + E)`                                        |
| Result of 2nd DFS Pass | One SCC per DFS tree                              |

---

## 🧪 Quick Quiz: Test Your Understanding

1. What is a strongly connected component?
2. Can a node belong to more than one SCC?
3. Why do we reverse the graph in Kosaraju’s algorithm?
4. What does the second DFS pass return?
5. What is the time complexity?

<details>
  <summary>✅ Show Answers</summary>

1. A group of nodes where all nodes can reach each other
2. ❌ No — each node belongs to **only one** SCC
3. To **uncover root nodes** of each SCC
4. All **SCCs** in the graph
5. **O(V + E)** — linear time

</details>

---

