# Tactical AI Combat — Minimax Alpha-Beta Demo

A lightweight, single-file browser game designed to demonstrate the **Minimax algorithm** with **Alpha-Beta pruning** in a practical, interactive way. You play as the Hero against a Dragon whose moves are calculated in real-time by the algorithm.

---

## 🎮 Overview

This project was built to visualize how adversarial search algorithms make decisions. Instead of a traditional grid-based game like Tic-Tac-Toe or Chess, this demo uses RPG-style turn-based combat. 

Every turn, the AI explores a game tree up to a specific depth (default is Depth 5) to predict future states, evaluating the best possible sequence of attacks, heals, buffs, and debuffs to defeat you.

## ✨ Features

* **Zero Dependencies:** 100% vanilla HTML, CSS, and JavaScript. No build tools or libraries required.
* **Real-time AI Analytics:** The UI displays live statistics for the algorithm's performance on every turn, including:
    * Nodes Evaluated
    * Nodes Pruned (via Alpha-Beta)
    * Pruning Efficiency (%)
* **Dynamic Combat System:** Includes status effects (buffs/debuffs) and randomized base damage variables to create a complex branching decision tree for the AI.

---

## 🛠️ How to Play

1. Save the provided code as an `.html` file (e.g., `index.html`).
2. Double-click the file to open it in any modern web browser.
3. Click **▶ Begin Battle**.
4. Choose your actions strategically to reduce the Dragon's HP to 0 before it does the same to you.

---

## ⚔️ Combat Mechanics

Both the Hero and the Dragon have 100 HP and access to the exact same set of moves:

| Move | Icon | Description |
| :--- | :---: | :--- |
| **Strike** | ⚔️ | Deals ~22 base damage to the opponent. |
| **Heal** | 💊 | Restores ~28 HP (cannot exceed the 100 HP maximum). |
| **Power Up** | ⚡ | Applies a **Buff**: Multiplies outgoing damage by **1.5x** for 3 turns. |
| **Weaken** | 🌀 | Applies a **Debuff**: Reduces opponent's outgoing damage by **0.6x** for 3 turns. |

*Note: Buffs and Debuffs do not stack, but their durations tick down each turn.*

---

## 🧠 Under the Hood: The AI

The Dragon's decisions are powered by the `bestMove()` and `mmx()` functions in the JavaScript block.

### Minimax Algorithm
The AI simulates all possible move combinations for both itself (maximizing score) and the player (minimizing score) up to 5 turns ahead. It evaluates the resulting board states using a custom heuristic function (`heur(s)`) that weighs the HP differences and active status effects:
* Positive scores strongly favor the Dragon.
* Negative scores strongly favor the Hero.
* Winning the game returns an artificially high maximum score (+9999).

### Alpha-Beta Pruning
Without pruning, evaluating 4 moves at a depth of 5 would require evaluating exactly $4^5 = 1,024$ nodes every turn. By tracking the best guarantees for both sides (Alpha and Beta), the algorithm "prunes" (skips) branches that are mathematically proven to be worse than a previously evaluated move. This vastly increases computational efficiency, which you can observe in the "Nodes Pruned" statistic on the game screen.
