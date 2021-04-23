
Created by: Eli Shieber, Sam Bieler, Michael Tylko
Class: ES 170
Date: 5/8/2019

----------------------
Overview
----------------------

This jupyter notebook runs A-Star search using a hybrid quantum-classical algorithm by replacing A-Stars priority Queue with an unordered list search done via Grovers algorithm.

Our jupyter notebook file includes:
	- Problem Creation
	- A classical A-star Implementation
	- A quantum A-star Extension of this implementation
	- Data Collection regarding the above

----------------------
Running Our Code
----------------------

To run each part of our run each cell in order. To quickly see a runthrough of our
algorithm run the demo section after running the previous cells.

We provide instructions for changing variables. We advise that you do not do this because it
is hard to change without really knowing the code.

Every function up to the function getPathCost is setup for later parts. Run this without
changing anything. The next cell sets up the grids for quantum data collection across
grids and varying number of grover checks. If you would like to you may change the i range to
set different grid size possibilities, and the j range in order to set how many grids of each
of those sizes are created. You can also change th range of j's inside of the next cell to
set the list of the number of checks that will be varied across for each grid. This cell can
then be run for quantum data collection. You can then run the next two cells in order to
create a graph of time versus number of checks from that data. If you would like you can insert
cells in this data, and inspect the other data collection variables that we created as seen as
empty lists at the top of that cell. Once you are satisfied with looking through that data you
can do the same process for the next cell for the data collection of quantum and classical data.
If you did not change the grids created, then all cells up to the demo can no be run without issue.
Otherwise, ensure that you have set all loops to the requisite values based on how you set the grid
creation loops. Also set all numpy array that are initialized with np.zeroes to have the length that is
equal to the difference in the size of largest and smallest grids you created. You may then run
everything up to demo.

If you would like you may now run the entire demo section.

----------------------
Problem Set Up
----------------------

These functions all serve to set up the problem space. Our A-star implementation runs on a
grid world with the start state in the top left corner of the grid, and the goal state in
the bottom left corner. gridCreatorNoObs creates a grid with no obstacles. gridCreator creates
a grid with a random number of obstacles. A-star search requires a heuristic to run, we
implement the manhattan distance heuristic in manhattanDist. Given a shortest path dictionary
returned by A-star, findOptimalPath will return a list of moves following the optimal path 
between two nodes. gridPrint will pretty print a grid. printGridPath will pretty print a 
grid with the revealed optimal path. getPath Cost will return the cost of a given path.

In amalgamation these functions are all that is needed to successfully implement and run
A-Star search classically.

Functions:
	
	gridCreator(size)
	gridCreatorNoObs(size)
	manhattanDist(start, end)
	findOptimalPath(paths, end, start)
	gridPrint(grid)
	printGridPath(path, grid)
	getPathCost(path, gridCosts)


----------------------
Classical A-star
----------------------

Classical A-star is implemented by the following functions. getActions returns the possible
future nodes to explore given what has already been explored, and your current location. Cost
returns the cost of taking an action. bInsert adds a node to the priority queue. aStarSearch combines all these functions in order to run A-star search clasically.

Functions:
	
	getActions(grid, curLoc, evaledSet)
	cost(start, end)
	bInsert(start, end)
	aStarSearch(grid, costDict)

----------------------
Quantum A-star Extension
----------------------

Quantum A-star Search is implemented in a very similar way to the classic approach, however the priority queue is replaced with a grovers implementation. pattern returns a controlled Z-gate necissary for creating a grovers oracle. createGroverOracle runs pattern and applies various other gates in order to create an oracle. groverSearch runs the grover search algorithm itself using the aforementioned functions

Functions:
	
	pattern(maxi, iterator, curList, qc, qr, piFrac)
	createGroverOracle(toMark, n, piFrac)
	groverSearch(grid, numChecks, costDict)


----------------------
Data Collection
----------------------

Data collection takes place in two parts:

	- Quantum A-star data collection on varying grid sizes and Number of min Grover Checks
	- Quantum and Classical A-star data collection on varying grid sizes with fixed number of min Grover checks

	each part includes timing data, path data, and node data.

Classical A-star data collection collects the following data:

	standardTimes = []
	standardPaths = []
	standardNodesEvaluated = []
	quantumPathCosts = []
	standardPathCosts = []
	gridStrings = []
	quantumPathStrings = []
	standardPathStrings = []
	standardInsertions = []
	standardRemovals = []

Quantum A-star data collection collects the following data:

	quantumTotalTimes = []
	quantumCircuitCreationTimes = []
	quantumPaths = []
	qubitCounts = []
	quantumNodesEvaluated = []
	quantumPathCosts = []
	gridStrings = []
	quantumPathStrings = []
	quantumInsertions = []
	quantumRemovals = []
	quantumChecks = []


----------------------
Demo Section
----------------------

This section contains a typical demonstration of both the classical, and our 
quantum implementation of A-star search. Included in this demo is the following:

	-create an empty example grid
	-print this grids heat map
	-create an example grid with obstacles and costs
	-print this grids heat map
	-find the optimal path according to classical A-star
	-print this optimal path
	-find the optimal path according to quantum A-star
	-print this optimal path
	-create arbitrary sized oracle
	-print this oracle
	-print gate sequence of this oracle

	



