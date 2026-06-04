6. Classical Heuristic Solution Procedures

In this section, we first describe approximation algorithms with a performance guarantee that were developed for TSPs with profits. We then present the main principles that underlie heuristic procedures. Some examples of procedures based on these components are given, as well as procedures driven by other principles. The following section presents metaheuristic approaches that make use of these components in a more effective fashion.

6.1. Approximation Algorithms with a Performance Guarantee

Awerbuch et al. (1998) derive an approximation algorithm for the PCTSP from an approximation algorithm for the k-minimum-spanning-tree problem (k-MST problem). The k-MST problem consists of finding a tree of least weight (distance) that spans exactly k vertices on a given graph. For the PCTSP solution, the authors propose replacing each vertex vi ∈ V with pi copies of itself at the same location and computing an approximate solution of the k-MST problem in this graph, with k = pmin. It only remains to classically double the computed tree to obtain a tour. Thus, the main topic of the Awerbuch et al. paper is an approximation algorithm for the k-MST problem. Their approximation algorithm achieves a factor O(log²(min(n, pmin))) for the PCTSP. This field of investigation has seen a huge development in the past few years, and several other papers have recently improved the approximation ratio for the k-MST problem, and consequently for the PCTSP (see Blum et al. 1999; Arora and Karakostas 2000; Arora 1998).

Bienstock et al. (1993) propose a polynomial approximation algorithm having a factor of 5/2 performance guarantee for the undirected PTP. In the first step of their algorithm, the linear programming relaxation of the problem is solved using the ellipsoid method and vertices vi with yi ≥ 3/5 are selected. A TSP heuristic with a worst case performance guarantee is then applied on this set of vertices. Goemans and Williamson (1995) improve the above performance guarantee and obtain a (2 − 1/(n − 1))-approximation algorithm with a purely combinatorial approach.

6.2. Main Principles of Heuristic Procedures

Unlike the classical TSP, the visit of every customer is not compulsory in TSPs with profits. Hence, routes limited to the depot as well as routes visiting all vertices are candidates for the solution. These two extreme types of routes are respectively optimal for the travel cost objective and the profit objective (independently of the sequence). At the same time, each one of them can possibly yield a very bad value for the other objective. Thus, the purpose of heuristic procedures is to balance the quality of both objectives. For this purpose, four main operations may be used to transform a route:

• Adding a vertex to the route
• Deleting a vertex from the route
• Resequencing the route
• Replacing a vertex of the route with a vertex outside the route.

In most cases, these operations lead to the improvement of one of the objectives at the expense of the other. An important question is how to manage these four operations to improve the quality of the solution, avoid local optima, prevent cycling.... All these points are discussed in the subsequent sections. For the moment, we present each one of these four operations. In the following, we note δ(p) and δ(c) the respective variations of profit and travel cost when a change is performed.

6.2.1. Adding a Vertex to the Route.

The addition of a vertex vi ∈ V to the route yields an increase δ(p) = pi of the quantity of collected profit, at the expense of increased travel costs. The best point to insert vi corresponds to the vertex vr for which the added cost δ(c) of visiting vi instead of its current successor vs, i.e., cri + cis − crs, is minimum.

The most effective criterion for choosing vi is seemingly to select the candidate vertex that maximizes δ(p)/δ(c). Yet the inconvenience of this criterion is that it does not anticipate future modifications of the route. Hence, Golden et al. (1987, 1988) have proposed several other criteria with which this primary criterion can be combined:

• A distance to the center-of-gravity measure, with different definitions for the center of gravity (center of gravity of all the vertices weighted by their profits, center of gravity of the vertices of the current route, center of gravity of a previously known route weighted by the profits)

• A distance to the destination measure

• A density measure, given by ∑vj∈V pj e−μcij, taking into account the density of profit around the vertex vi, where μ is a parameter chosen to reflect the scale of intervertex distances.

All these measures attempt to attract the route toward vertices that seem promising for future modifications. This idea is rather original and is not found in insertion heuristics for the TSP where all vertices have to be included in the route.

Similarly, note that Ramesh and Brown (1991) develop the idea of a double insertion and that Gendreau et al. (1998b) extend it to the insertion of clusters.

6.2.2. Deleting a Vertex from the Route.

The deletion of a vertex vi ∈ V of the route leads to decreased travel costs, at the expense of decreased δ(p) = pi collected profit. As for the insertion, the variation of travel costs is δ(c) = cri + cis − crs, where vr and vs are the neighbors of vi in the route and a natural criterion is to select a vertex vi ∈ V that minimizes δ(p)/δ(c).

Ramesh and Brown (1991) propose extending this principle and assessing the deletion of every vertex followed by some 2-opt interchanges. The vertex that minimizes the profit-to-savings ratio is deleted. The same idea could be applied for the insertion of vertices.

6.2.3. Resequencing the Route.

Resequencing a route always leads to a better solution because it may decrease travel costs while leaving profit unchanged. It amounts to simply considering the set of vertices currently visited by the route and trying to shorten the length of the route through these vertices. Hence, we are exactly in the situation of an improvement procedure for the classical TSP.

The TSP solution procedures used by the researchers for TSPs with profits are the 2-opt procedure of Lin (1965, see Chao et al. 1996a), the 3-opt procedure of Lin (1965, see Ramesh and Brown 1991), and the GENIUS algorithm of Gendreau et al. (1992; see Gendreau et al. 1998b). Actually, the field of improvement procedures for the TSP has seen a lot of attention, and many effective procedures, mostly based on Lin’s k-opt mechanism, are available, the question being how much time one is ready to spend for improvement. Nevertheless, note that Tsiligirides (1984) and Keller (1989) develop routines of their own.

6.2.4. Replacing a Vertex.

Another possibility is to swap two vertices, one belonging to the route and one outside the route. Whatever the TSP with profits, it is a pure improvement procedure if one limits swapping to pairs of vertices such that δ(p) ≥ 0 and δ(c) ≤ 0. However, less-drastic conditions are sufficient to ensure improvement for each type of TSP with profit. For instance, one can consider substitutions that increase profit provided that the route remains feasible in the context of the OP (Tsiligirides 1984). Note that Keller (1989) extends this scheme by authorizing the deletion of two consecutive vertices and that Dell’Amico et al. (1998) propose deleting a chain.

6.3. Classical Heuristics

Many heuristic procedures are obtained with a clever combination of the components described above. However, mixing these components may induce some difficulties, in particular, cycling. Some procedures that we present below iteratively apply the basic steps described above, with a descent strategy:

• Greedy insertion procedures consist of iteratively inserting vertices in a route until no more vertices can be added (OP), the solution is feasible (PCTSP), or no improvement is possible (PTP). Initially, the route is restricted to a loop around the depot. These procedures can easily be combined with resequencing or vertex swapping to decrease the travel costs at some steps of the solution procedure or when insertions are no longer possible.

• The equivalent greedy deletion procedures are also possible. The initial route is then a TSP solution. For the PTP, note that insertion and deletion can be applied simultaneously, with the best candidate vertex for a modification being selected at each step, as proposed by Mittenthal and Noon (1992).

• Based on these ideas, Dell’Amico et al. (1998) present two heuristic procedures for the PCTSP. In the first one, the Lagrangian relaxation of the knapsack constraint and the solution of the resulting PTP instances yield an initial route. Insertion is then used to attain feasibility of the route. The route is improved afterward with two procedures, extension and collapse, that are applied iteratively until no further improvement is possible. Extension applies insertion as long as insertions are over a computed average ratio. Collapse carries out the replacement of a chain by a single vertex. The second heuristic uses the same components, but in a different order. In particular, the extension and collapse procedures are applied during the optimization of the Lagrangian dual. This second heuristic proves to be more effective, especially when the resource constraint is naturally satisfied, since, in this case, the Lagrangian optimization often directly provides a feasible solution.

Besides the previous heuristics, other approaches have been developed for the solution of TSPs with profits:

• Path-extension procedures: These construction procedures involve extending a path until no more vertices can be added (OP). They are faster but less effective than the equivalent greedy-insertion procedures. However, because of their efficiency, a randomized behavior can be introduced by selecting one of the most promising vertices in a probabilistic fashion (Tsiligirides 1984). It enables one to repeat the procedure many times and to select the best solution. Even so, the myopic behavior of the extension is quite detrimental, and this procedure does not provide very good solutions.

• Sweep-based procedure: Tsiligirides (1984) proposes a solution approach based upon the sweep algorithm (Wren and Holliday 1972) for the TSP. The geographic area is divided into sectors determined by two concentric circles and an arc of given length. Sectors are changed by varying the two radii of the circles and rotating the arcs. Routes are built up within each of the sectors. Many cases are examined and the best route is selected. This heuristic is compared with the stochastic path extension procedure described above. For similar computing times, results are clearly inferior for the sweep approach.

• Partitioning-based procedure: Unlike previous methods, Chao et al. (1996a) do not focus on a single route, but try to improve the best route among a set of feasible routes. Vertices are partitioned in a set of feasible routes, where the best route is emphasized. Two local search procedures are described. In the so-called two-point exchange procedure, each vertex of the best route is considered in sequence. It is possible to move the vertex to another route while in return a vertex of this route moves to the best route. In the so-called one-point movement procedure, every vertex of every route is considered in sequence. This time, it is just possible to move it to another route. In both procedures and for each considered vertex, moves are made as soon as the highest profit among the set of routes increases. An important point is that the best route might change during the process.
