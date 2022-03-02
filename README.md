# README
This is exploration algorithm code based on papar [Coordinated Multi-Robot Exploration](http://www2.informatik.uni-freiburg.de/~stachnis/pdf/burgard05tro.pdf).

Algorithm 1, presented here, is a method of selecting a target point using cost and utility.

Cost function is obtained as follows: the value function of each cell is obtained using value iteration, which is a popular dynamic programming algorithm. It corresponds to the cumulative cost of moving from the current position of the robot to that cell.

Utility function is obtained as follows: First, let all frontier cells have the same utility. Each time a frontier cell is occupied by a robot, the utility of all frontier cells is reduced, and the degree of decrease depends on the distance to that frontier cell occupied.

The smaller the cost and the higher the utility, the higher the probability of becoming a target cell. Algorithm 1 assigns that target location to a robot which has the best tradeoff between utility and costs.

# AUTHORS
The original author of this code is **QuinnSpearman**. I will skip COPYING/LICENSE by attaching the Github code HTTPS: https://github.com/QuinnSpearman/Coordinated-Multi-Robot-Exploration.git

And I made this code by adding cost function to that code.

# INSTALL
The code works normally only when *pygame*, *scipy* packages are installed and *arrow.png* is downloaded in advance.

# NEWS
To consider cost function, I calculated the value function of all cells by implementing the principle of value iteration as a code. 

I applied the cost to the utility function so that the smaller the value function of a frontier cell, the greater the preference of the robots.

# ChangeLog
1. Set *value* and *minvalue* method for all classes so that value function is initialized according to the type of cell.
2. Add the code implementing the value iteration to the line 721 to 735. According to this code, the value function of each cell is updated by the value function of its neighbor cells and the distance to those cells. Here, the probability of each cell being occupied is fixed at zero point one. And iteration should be repeated until convergence originally, it is repeated only five times due to the complexity of the calculation.
3. In line 801, *minvalue* of each cell updated through value iteration is stored in the variable *cost*.
4. In line 804, cost function is applied by subtracting the *cost* from the existing utility function. Here, I change the constant multiplied by the cost function to find out which constant has the least exploration time.

# BUGS
When initially setting the location of the robot, **IndexError: list index out of range** sometimes occurs. Even if the robot is placed in the same location, errors appear randomly in one out of five times.

# TODO
- I would like to analyze the cause of BUGS and correct them.
- When cost is applied, the calculation time increases exponentially due to the complexity of value iteration. So I plan to reduce it by calculating value iteration in a different way.
- I implemented a code that controls one robot to determine a target cell and then the other robots to be unable to select that cell. The results showed that the exploration time was longer than that of the algorithm 1, but the experimental conditions were limited. I plan to experiment again based on more diverse conditions.

- I want to create cases where obstacles move or the environment changes over time.
