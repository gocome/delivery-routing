# delivery-routing
Find the shortest total distance of routes to deliver demands. 
It is a well-studied Capacitated Vehicle Routing Problem (CVRP).


### Problem description
Two trucks are tasked to deliver goods from a depot to 20 customers at different locations.
The pair-wise distances between customers (and the depot) are precomputed 
and provided in a distance matrix of size [21x21], together with a custom demand list of length 20.
Both trucks have the same load capacity limit of 100.


The objective of this problem is to find two routes, one for each truck, such that
- the total traveling distance of two routes is as short as possible,
- each route shall start from the depot and end at the depot as well,
- every customer locations shall be visited in order to deliver the command, and
- each truck's load must not exceed its capacity limit at any time of delivery.

### How to run code
1. Clone the repository `delivery-routing` from GitHub to a local machine
```commandline
git clone https://github.com/gocome/delivery-routing.git
```
2. Create a virtual environment with Python 3.8 and then install the required packages 
```commandline
pip install -r requirements.txt
```
3. Run the file `main.py` to output the optimal delivery routes
```commandline
python main.py
```

### Experimental results
The above running procedure will give the following output.

```text
Objective: 215

Route for truck 0:
 0 Load(92) ->  5 Load(83) ->  14 Load(74) ->  6 Load(63) ->  10 Load(53) ->  9 Load(45) ->  19 Load(35) ->  13 Load(30) ->  4 Load(15) ->  3 Load(8) ->  1 Load(0) ->  0
Distance of the route: 106
Load of the route: 92

Route for truck 1:
 0 Load(98) ->  11 Load(91) ->  12 Load(78) ->  17 Load(70) ->  8 Load(56) ->  7 Load(50) ->  18 Load(39) ->  16 Load(33) ->  15 Load(21) ->  20 Load(12) ->  2 Load(0) ->  0
Distance of the route: 109
Load of the route: 98

Total distance of all routes: 215
Total load of all routes: 190
```

There are two routes reported, one for each truck. 
The first truck delivers a total demand of 92 to 10 locations, while the second truck delivers a total demand of 98 to the rest 10 locations. So, the maximum load of each truck did not exceed its capacity limit of 100.
The traveling distances of two routes are 106 and 109, respectively, giving rise to a total distance of 215 (which is also the objective value that the algorithm found).

### Discussions
1. Code was basically modified from https://developers.google.com/optimization/routing/cvrp.
2. The input data to the program shall be provided in the file `cvrp_problem_data.json`, which is located under the subfolder `data`.
3. We additionally assume that each truck services at most one route in the algorithm.
4. To have a feasible solution, the total capacity of all trucks shall not be less than the total demands of all the delivery locations.
5. The algorithm used meta-heuristic to search for routes, so the optimal routes are not guaranteed to be found. However, it has been shown that the solution is within 1% of the optimum for a problem instance of large size (https://en.wikipedia.org/wiki/Vehicle_routing_problem).
6. The current code can easily adapt to the more general case in which there are more than two trucks and/or trucks have different capacities.
7. The CVRP generalises the Vehicle Routing Problem (VRP), which further generalises the Travelling Salesperson Problem (TSP). Therefore, the CVRP is computationally intractable.