# ⬡ Independent Set — NP-Completeness Visualizer

> An interactive web-based tool for exploring the Independent Set problem, its algorithms, and its NP-completeness proof — built as a companion to coursework in algorithmic analysis.

**Live demo:** [leannejrodrigo.github.io/independentset-visualizer](https://leannejrodrigo.github.io/independentset-visualizer/)

---

## Overview

The Independent Set problem asks: given an undirected graph **G = (V, E)** and an integer **k**, does there exist a subset **S ⊆ V** with **|S| ≥ k** such that no two vertices in S share an edge?

This visualizer makes that abstract question concrete. It lets you load or construct graphs, step through two algorithms frame-by-frame, read a full NP-completeness proof, and compare the behaviour of exact versus heuristic approaches — all in a single-page app with no dependencies or build step.

---

## Features

### 📊 Overview Tab
- Formal problem definition with the decision-problem formulation
- Intuitive party-guest analogy and real-world applications (wireless channel assignment, register allocation, scheduling, etc.)
- Complement relationship between Independent Set and Vertex Cover
- Worked step-by-step greedy trace on a five-vertex graph
- Complexity comparison table (Brute Force vs. Greedy)

### 🔵 Algorithm Visualizer
- **Graph input** — six built-in presets (Cycle C₅, Petersen-Like, Bipartite K₃‚₃, Path P₆, Dense Graph, and a verified Greedy Counterexample), custom edge entry, or a random graph generator (2–20 vertices, four density levels)
- **Two algorithms** — Greedy Min-Degree heuristic (O(n² + nm)) and Brute Force exact search (O(2ⁿ · n²), capped at n ≤ 14)
- **Step-by-step playback** — play, pause, step forward/back, jump to any step, and adjustable speed (100–2000 ms per step)
- **Live pseudocode panel** — active line highlighted in sync with the graph; hover any line for a tooltip explaining that line's purpose and local complexity
- **Step history log** — colour-coded by event type (INIT / CONSIDER / SELECT / ELIMINATE / DONE), clickable to jump to any past state
- **Node colour legend** — Unvisited, Considering, In Independent Set, Eliminated, Removed
- **Complexity growth chart** — interactive canvas plot of O(2ⁿ) vs. O(n²) on a log scale; drag the slider to extend the x-axis up to n = 40; current graph size shown as a dashed marker

### 🔬 NP-Completeness Proof
Collapsible accordion proof covering:
1. Key definitions (Graph, IS, Vertex Cover, NP, NP-Hard, NP-Complete)
2. **IS ∈ NP** — certificate + O(n²) polynomial-time verifier with pseudocode
3. **NP-Hardness** — polynomial-time reduction from Vertex Cover: (G, k) → (G, |V| − k)
4. Correctness — forward direction (VC ⇒ IS) with SVG path diagram
5. Correctness — backward direction (IS ⇒ VC) with biconditional summary
6. Conclusion table and nested complexity diagram (P ⊂ NP ⊃ NP-Complete)
- **Interactive reduction calculator** — enter |V| and k, outputs the corresponding IS instance with correctness explanation

### ⚡ Algorithm Comparison Tab
- Side-by-side pseudocode panels (Greedy and Brute Force) with the same hover-tooltip system
- Greedy paradigm design rationale and approximation guarantee discussion
- Proven counterexample diagram (8-node graph, Greedy finds IS of size 3, Optimal is 4)
- **Live side-by-side comparison** — pick any preset, click "Run Both Algorithms", and see both results rendered simultaneously with an analysis banner indicating whether Greedy found the optimal solution or fell short

---

## Algorithms Implemented

| Algorithm | Time Complexity | Space | Optimal? |
|-----------|----------------|-------|----------|
| Greedy Min-Degree | O(n² + nm) | O(n + m) | Not guaranteed |
| Brute Force (bitmask) | O(2ⁿ · n²) | O(n) | Always |

**Greedy strategy:** at each iteration, pick the vertex with the lowest degree in the current active subgraph, add it to the independent set, then remove it and all its neighbours. Ties are broken by vertex index.

**Brute force strategy:** enumerate all 2ⁿ subsets using a bitmask; for each subset check all pairs for edges; track the largest valid independent set found.

---

## NP-Completeness at a Glance

```
Independent Set is NP-Complete because:

1. IS ∈ NP      — given subset S, verify |S| ≥ k and no edges in S×S in O(n²)
2. IS is NP-Hard — Vertex Cover ≤_p IS via: (G, k) → (G, |V| − k)
                   S is an IS  ⟺  V \ S is a Vertex Cover (complement relationship)
```

The report also proves a separate reduction from **Clique** to Independent Set using the complement graph construction: a clique of size k in G becomes an independent set of size k in the complement Ḡ, and vice versa.

---

## Getting Started

No build tool or package manager needed. The entire application is a single self-contained HTML file.

```bash
git clone https://github.com/leannejrodrigo/independentset-visualizer.git
cd independentset-visualizer
open index.html        # macOS
# or just double-click index.html in your file manager
```

To serve locally (avoids any browser file-protocol quirks):

```bash
python3 -m http.server 8080
# then open http://localhost:8080
```

---

## Project Structure

```
independentset-visualizer/
├── index.html          # entire application — HTML, CSS, and JS in one file
├── report.pdf          # full written analysis (BCS 309 — Algorithms I)
└── README.md
```

---

## Academic Context

This visualizer was developed as a companion tool for **BCS 309 — Algorithms I** at the School of Engineering, Applied Sciences and Technology, under the supervision of Dr. Arash Kermani.

The accompanying written report provides the full formal analysis behind everything implemented in this tool.

📄 **[View Full Analysis (PDF)](./report.pdf)**

The report covers:
- Formal problem statement with YES and NO examples
- Brute-force analysis: why the 2ⁿ factor arises from subset enumeration
- Polynomial-time verifier: O(n²) pairwise check establishing IS ∈ NP
- Greedy min-degree heuristic: O(n³) upper-bound derivation and approximation limitations
- Polynomial-time reduction from **Clique** to Independent Set via complement graph, with a four-vertex worked example and full correctness proof in both directions

---

## Tech Stack

- **Vanilla HTML / CSS / JavaScript** — zero runtime dependencies, zero build step
- **SVG** for all graph rendering and static diagrams
- **Canvas API** for the complexity growth chart
- CSS custom properties for theming throughout

---

## License

This project was created for academic purposes. Feel free to use it as a study or teaching reference.
