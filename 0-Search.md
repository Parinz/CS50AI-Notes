# Search Problems

A search for a solution that a computer can do.

> Tic Tack Toe, Google Maps

-   Agent: An **entity** that percieves env and makes decision.
-   State: **Configuration** of the _environment and the agent_.
-   Actions: **Functions** that the entity can take to lead to the goal.
    -   _ACTIONS(s)_ returns available actions in **state (s).**
-   Transitional Model: **Resulting state** that comes from actions.
    -   _RESULT(s, a)_ returns state from action _a_ from state _s_.
-   State Space: **Set of all states** --> _Graph_
-   Goal Test: Determine if state is **goal state**
-   Path Cost: **Cost** that comes from actions.
-   Optimal Conlusion: **Best** possible actions.
-   Frontier: **All possible actions** from the state.

## Node

A data structure that keeps track of:

-   State
-   Parent
-   Action from Parent
-   Path Cost

```python
class Node():
    def __init__(self, state, parent, action):
        self.state = state
        self.parent = parent
        self.action = action
```

## Approaches

1. Start with a _frontier_ with the **initial state**.
2. Start with empty _explored set_.
3. Repeat:
    1. _Frontier_ == empty -> No solution
    2. Remove _node_ (go explore that one)
    3. If node is goal, _return solution_
    4. Add node to _explored set_.
    5. Expand _node_ (Consider all possible actions) if not in _explored set_ or in there already.

# Uninformed Search

Algorithms such as _BFS or DFS_, **have no problem-specific knowledge**.

-   No idea what the data-strcutures or anything are.

## Depth-first Search

Using a **_Stack_**:

-   Last-in first-out data type.

```python
class StackFrontier():
    def __init__(self):
        self.frontier = []

    def add(self, node):
        self.frontier.append(node)

    def containsState(self, state):
        return any(node.state == state for node in self.frontier)

    def empty(self):
        return len(self.frontier) == 0

    def remove(self):
        if self.empty():
            raise Exception("Empty Frontier")
        else:
            node = self.frontier[-1]
            self.frontier = self.frontier[:-1]
            return node
```

### Maze

In a maze it will go into the deepest path.

## Breadth-first Search

Using a **Queue**:

-   First-in first-out data type.

```python
class QueueFrontier(StackFrontier):
    def remove(self):
        if self.empty():
            raise Exception("Empty Frontier")
        else:
            node = self.frontier[0]
            self.frontier = self.frontier[1:]
            return node
```

### Maze

Instead of exploring one path, it will:

-   Explore **each path all at once** with picking the shallowest path each time.
-   The problem is that it would go into **every thing**.

---

# Informed Search

**Have problem-specific knowledge.**

-   Knowing that being in a cube closer to coordinate is better.

## Greedy Best-first Search

Expands node that _thinks_ it is **closer to the answer**. --> **Hueristic function _h(n)_**

-   Problem is that it may always not get the optimal answer.

### Heuristic Function

Tries to **estimate** which way is _better_.

**Manhattan Distance**: Heuristic function that goes grid my grid, and can not go diagonally.

## A\* Search

Expands node with lowest value of **_g(n) + h(n)_**

-   **g(n)** = cost to reach node (current postition)
-   **h(n)** = estmiated cost goal

**It also explores _at the same time_.**

### Conditions

-   **h(n)** never _overestimate (is admissable)._
-   **h(n)** is _consistent_

---

# Adversarial Search

-   A type of search where you are **fighting against something.**

We have to translate the _game_ to the computer.

## Minimax

Assigning numbers to _Tic Tack Toe_:

-   **O** wins **-1**
-   Tie **0**
-   **X** wins **1**

1. The **X** player wants to _maximize_, **MAX(X)**
2. The **O** player wants to _minimize_ **MIN(O)**

### Game

-   _State 0_ -> Initial state
-   _Players(s)_ -> Return which player to move in current state
-   _Actions(s)_ -> Return possible moves
-   _Result(s,a)_ -> Return state after action is taken in current state
-   _Terminal(s)_ -> Check if game has ended.
-   _Utility(s)_ -> Find numerical value from state

### Alpha-Beta Pruning

Not checking all the choices, **if you see a low number** then skip.

## Depth-Limited Minimax

Instead of searching through the whole search tree, stop searching.

-   _Evaluation Function_ -> Function that estimates expeced utility from a given state.
