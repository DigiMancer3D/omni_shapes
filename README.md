# Omni Shapes: Unlock Infinite Patterns in Polyominoes & Beyond! 🚀

[![GitHub license](https://img.shields.io/github/license/DigiMancer3D/omni_shapes?style=for-the-badge)](https://github.com/DigiMancer3D/omni_shapes/blob/main/LICENSE)
[![GitHub stars](https://img.shields.io/github/stars/DigiMancer3D/omni_shapes?style=for-the-badge)](https://github.com/DigiMancer3D/omni_shapes/stargazers)
[![GitHub issues](https://img.shields.io/github/issues/DigiMancer3D/omni_shapes?style=for-the-badge)](https://github.com/DigiMancer3D/omni_shapes/issues)
[![GitHub forks](https://img.shields.io/github/forks/DigiMancer3D/omni_shapes?style=for-the-badge)](https://github.com/DigiMancer3D/omni_shapes/network)
[![Contributors welcome](https://img.shields.io/badge/contributors-welcome-brightgreen.svg?style=for-the-badge)](https://github.com/DigiMancer3D/omni_shapes/blob/main/CONTRIBUTING.md)

> **Play the Demo Now!** 🎮  
> Dive right in and start building shapes interactively: **[Try Omni Shapes Live](https://3dd.in/Omni)**  
> *<sup><sub>&nbsp;&nbsp;&nbsp;&nbsp;Live Demo May Not Reflect Most Recent Build Version</sub></sup>*     </br>
> (Pro Tip: Enable GitHub Pages on this repo for a direct link like https://digimancer3d.github.io/omni_shapes/omni_shapes.html)

Welcome to **Omni Shapes**, your gateway to exploring "Omni Shapes" — a revolutionary coordinate-based system for polyominoes and multi-dimensional puzzles! Forget rigid matrices; we use relative coordinates for effortless rotations, mirrors, and jumps to 3D/4D. Perfect for puzzle lovers, coders, and math wizards.  

If you're excited about algorithms, geometry, or hacking on open-source fun, fork this repo and join the adventure! We've got bugs to squash, features to add, and shapes to discover. Let's collaborate and expand the universe of patterns together. 🌌

---

## 📑 Table of Contents

- [🌟 Overview](#-overview)
- [🛠️ How It Works](#️-how-it-works)
  - [Core Concept: Coordinate-Based Tracking](#core-concept-coordinate-based-tracking)
  - [Grid Setup and User Interaction](#grid-setup-and-user-interaction)
  - [Color-Coding System for Click Allowance](#color-coding-system-for-click-allowance)
  - [Tracking Pick Numbers with DOM Variables](#tracking-pick-numbers-with-dom-variables)
  - [Determining Alt-Moves (Missed Opportunities)](#determining-alt-moves-missed-opportunities)
  - [Mathematical Determination of Mirrored Position Graphs](#mathematical-determination-of-mirrored-position-graphs)
- [🔥 Unique Systems and Functions](#-unique-systems-and-functions)
- [🐛 Known Bugs](#-known-bugs)
- [🚀 Desired Upgrades](#-desired-upgrades)
- [👩‍💻 How to Run and Contribute](#-how-to-run-and-contribute)
- [📜 Rules and Explanations](#-rules-and-explanations)
- [🖼️ Visuals](#️-visuals)
- [📄 License](#-license)

---

## 🌟 Overview

Omni Shapes flips the script on polyomino discovery by using **relatable coordinates** over visual grids. Start with a base, track position changes, and boom — shapes that rotate, mirror, and scale to higher dimensions effortlessly.  

Think: A 2D "L" shape as `(4,4) [+0,-1] [+0,-1] [+1,0] (5,2)`. This unlocks "free" polyominoes without symmetry headaches.  

Our web tool (`omni_shapes.html`) lets you build on a grid, enforce rules, spot alternatives, and generate mirrors in real-time. Ready to shape the future?  

---

## 🛠️ How It Works

Powered by HTML, CSS, and JS, this interactive grid turns shape-building into a game. "Clones" explore paths, colors guide moves, and math handles transformations.

### Core Concept: Coordinate-Based Tracking

Ditch matrices — use **change arrays**: `start [changes] end`. Deltas (e.g., x,y) make transformations a breeze. Extend to 3D? Just add axes!

### Grid Setup and User Interaction

JS builds a dynamic grid (default 9x9). Click to place, validate adjacency, and update visuals.

### Color-Coding System for Click Allowance

- ⚪ **Available**: Adjacent, rule-compliant.
- 🔵 **Proofs**: Proof Digits.
- 🟡 **Potential**: Potential alt-moves.
- 🟢 **Placed**: Your shape so far.
- 🟣 **Alt-Moves**: Alt-Moves taken by system.

Simplifies logic with instant feedback.

### Tracking Pick Numbers with DOM Variables

Picks start at 1, stored in `data-pick` attrs. Globals track state; proofs in `data-proof` limit futures.

### Determining Alt-Moves (Missed Opportunities)

Scan adjacents, simulate clones for 1-step alternatives. (Deeper recursion? Coming soon!)

### Mathematical Determination of Mirrored Position Graphs

Flip signs, swap axes, apply rotations (e.g., 90°: x=y, y=-x). Normalize for uniques — pure math magic!

---

## 🔥 Unique Systems and Functions

- **Proof Digits**: Boundary trackers with dimensional twists.
- **Clone Simulation**: Path exploration without commits.
- **Multi-Dim Extensions**: Add axes seamlessly.
- **Pattern Swapping**: Mix known shapes.

Key funcs: `buildGrid()`, `handleCellClick()`, `findAltMoves()`, `generateMirrors()` — modular for hacks!

---

## 🐛 Known Bugs

Transparency first! Fix these and earn contributor cred:

<s>1. **Grid Size Glitch**: Non-9 sizes mess up proof fills (hardcoded offsets?).</s></br>
2. **Shallow Alt-Moves**: Only 1-click deep; misses multi-step.

Potentials: High-dim overflows, large-grid perf, input validation.

Spot more? [Open an Issue](https://github.com/DigiMancer3D/omni_shapes/issues)!

---

## 🚀 Desired Upgrades

Level up Omni Shapes:

- **Export/Import Shapes**: JSON save/load for shape libraries. (Use Blobs/FileReader!)
- Auto-gen all shapes to N, 3D viz (WebGL), AI suggestions.

Code snippet for export:
```javascript
function exportShape() {
  const shapeData = { start: [4,4], changes: [[0,-1], [0,-1], [1,0]], end: [5,2] };
  const blob = new Blob([JSON.stringify(shapeData)], { type: 'application/json' });
  const url = URL.createObjectURL(blob);
  const a = document.createElement('a');
  a.href = url;
  a.download = 'omni_shape.json';
  a.click();
}
