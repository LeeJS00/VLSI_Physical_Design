# VLSI_Physical_Design
This is the main points of the book, VLSI Physical Design.

## 1. Introduction

- Introduce & evaluates alogorithm during physical design
- digital cirtuits.
- EDA(Electronic Design Automation)
    - new IC designs

---

## 2. Netlist and System Partitioning

- Efficient cut makes efficient external connections
- Subgraph & nodes ⇒ block & cut set
- Graph G(V,E), v ∈ V, v has s(v) : area, e ∈ E, e has w(e) : weight
    - Divide Graph G in to k subgraphs
    - number of Connections btw partition minimize :  | cut set | min
    - Each particion meets all design constraints
    - Balace partition
    - NP-hard prob
- KL Algorithm : based on edges
    - same number partition
    - cost D(v) = | Ec(v) | - | Enc(v) |, v ∈ V
    - Ec(v) : incident edges cut by cut line, Enc(v) : edges X cut by cut line
    - D > 0, node move, D < 0 OK
    - gain of swapping pair △g = D(a) + D(b) - 2 * c(a,b) : c w(a,b)
    - Do while G > 0, G = ∑ △g. Max G is the best
    - O(n^3) per pass
- FM Algorithm : based on nets
    - X same number partition
    - △g = FS(c) - TE(c)
        - FS : moving force. # of nets connected to c, X connected by other sells within C's partition
        - TE : retention force. # of uncut nets connected to c
        - △g higher, move
    - G = ∑ △g. Max G is the best
    - ratio factor
        - r = area(A) / (area(A) + area(B))
        - balance : r * area(V) - maxarea(V) ≤ area(A) ≤ r*area(V) + maxarea(V)
    - base cell : △g max
    - O(n) per pass
- Multilevel partitioning
    - Clustering
    - FM partitioning

---

## 4. Global and Detailed Placement

- Placement goal : determine the locations and orientations of all circuit elements
    - movable(placeable elements determine quality
- For large circuits : global placement, detailed placement, legalization
    - Global
        - neglect shape or size
        - overlap allow
    - Detailed : legalization
        - seek to align
        - remove overlap
        - minimize displacemnet
- Optimization Objectives
    - total wirelength
        - HPWL model : make smallest rectangle encloses pin locations
            - fast, equal length of RSMT 2, 3 pin
            - maring of error
        - clique graph
        - Monotone chain
        - star model
        - RMST
        - RSMT
        - RSA
        - STST
    - Number of cut nets
        - cutline으로 cut을 나누어 netline 과 crossing
        - minimize cut crossing
        - cut size X(p) = max(# of vertical crossing), Y : horizontal
    - wire congestion(density)
        - ratio of demand for routing tracks
        - wire density Φ(e) of edge e = estimate # of net cross e / maximum # of net cross e
        - Φ ≤ 1 : routable, Φ > 1 detour some nets
    - signal delay
        - AAT(Actual Arrival Time), RAT(Required Arrival Time)
        - AAT ≤ RAT
- Global placement
    - Partitioning-based algorithm
        - min-cut placement - KL, FM
        - pros : fast, hierarchical strategy
        - cons : randomized
    - analytic placement
        - quadratic placement
            - connection : euclidean distance
            - solving local minimum
            - pros : math solve, eff algo, X use netlist clustering, stable
            - cons : fixed object necessary
        - force-directed placement
            - define Force as vector
            - finding 무게중심
    - stochastic algorithm
        - simulated annealing
        - back propagation
    - mordern placement algorithms
        - quadratic placers
            - large, sparse system conjugate gradient
            - use fake nets to remove dense region
        - non-convex optimization placers
            - slow
- Legalization and detailed placement
    - Legalization : find legal placemnet
    - use detailed placement
        - swapping cells
        - sliding cells to unused space

---

## 5. Global Routing
