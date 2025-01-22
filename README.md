# Swarm Intelligence:

I wanted to make a presentation about Swarm intelligence because I discover while doing my research on techniques to solve TSP that an algorithm inspired by ants can be used and is very efficient. After that I wondered if other algorithm were inspired by animals, and a lot of algorithm are actually inspired by insects and their collective intelligence which I found fascinating.

## Research:

Introduction to Swarm Intelligence - GeeksforGeeks
The concept was introduced by Gerardo Beni and Jing Wang in the year 1989. Illustrating that a group of object(animal,humain,…) are able to found better solutions when they work in groups (swarm). The idea is that each individual will participate using his own knowledge to building a solution/ an answer.
Swarm Intelligence: Algorithms, Applications, and Real-World Use Cases | by Abhilash Krishnan | Medium
Describe the concept of diverse algorithm
https://www.bing.com/ck/a?!&&p=0f64b63810c8e7cab67da9e5f6c67af2710ac85e87c08f4546ad9f2d1bd5f3faJmltdHM9MTczNjIwODAwMA&ptn=3&ver=2&hsh=4&fclid=1ef6cac8-20cd-66fc-1211-de43217467be&psq=swarm+intelligence+algorithm&u=a1aHR0cHM6Ly93d3cucmVzZWFyY2hnYXRlLm5ldC9wdWJsaWNhdGlvbi8yNjQ0NTc3NzVfU3dhcm1fSW50ZWxsaWdlbmNlX0NvbmNlcHRzX01vZGVsc19hbmRfQXBwbGljYXRpb25z&ntb=1
Ant Colony Optimization
Ant colony optimization: A bibliometric review - ScienceDirect
Constant augmentation on the interest of this program
  
Most used metaheuristic with PSO
Introduction à l'optimisation des colonies de fourmis - GeeksforGeeks
 
The main idea of ACO is that ants are going from there colony to the food source using various paths. On their way they leave pheromones behind them. When they want to go back to the colony after finding food they tend to pass through paths with higher quantity of pheromones and leave more pheromones behind them. 
Ants who took the shorter path arrive first at the food source and tend to go back by the way they went doubling the pheromones on the fastest path. Pheromones evaporates with time and usually ants end up using mainly one or a small number of paths.
This is the pseudocode propose in this documentation
 ![image](https://github.com/user-attachments/assets/464ec1b8-2602-4d66-b1d4-cc654001f401)

The pheromones values are initialize the same way on each path at the beginning and are then updated each iteration depending on the number of ants taking the path and the evaporation rate.
This local search method depends on different parameters such as the number of ants in the colony or the evaporation rate of the pheromone.

## My Algorithm

To illustrate the performance of swarm intelligence I decided to code two algorithm. (stopped codding the second one when I was not selected to present the project).
The one I have completely code for this presentation is Ants Colony Optimization for TSP problem. I evaluated it by using the same dataset used in Lab2.
The algorithm is composed of two functions the main one AntColony and the other one Next_city.

I started from my greedy algorithm function for TSP and adapted it to match the ACO format. 
The Ant Colony function takes as input the 2D tab distances regrouping each couple of city associated with the distance in kilometre between them (this was already created in lab2). It also take the evaporation rate of the pheromones (between 0 and 1), the higher this value is the faster the pheromones will evaporates. Finally it takes the number of ants in the colony and the maximum number of iteration.

We start by initialise the best solution as None, the best value (length of shortest path) as infinite and the pheromones as 1 on each path between each possible couple of cities. We keep track of the pheromones in a matrix pheromones (similar shape as the distances).

Then for each iteration we are going to determine the solutions provided by all ants. Each ant will start from a random city (this is really important at the beginning because when I made them start from the same cities the model was way less efficient). Then they will select the next city and move to it and repeat until having visited every city. The next city is determined using the next_city function which will calculate the probability of each city to be selected by dividing the pheromones of the path (current city,next city) by the square of the distance. It is important to say that there is many way to determine the probability with ACO giving more or less importance to the pheromones and distances. I first tried dividing the pheromones by the distances but the model did not converge properly. Then we nomalize the probability (sum of proba equal one). Finally the next city is randomly chosen (using the probability as weight) to be return.
When a path has been calculated for each ant of an iteration we will update the pheromones. First by evaporing the existing one on each road. Then we add one pheromone inversely proportional of the coast of the path for each used road. Finally we select the best solution yet found (all iterations) and add a pheromone in this path as well. In the end the function return the best path, it’s value and the fit list (list of best path at found at each iteration.

