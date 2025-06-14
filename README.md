# AI-assignment-1---CT421
# Set up instructions
## Requirments
- This notebook Uses `tsplib95` for loading TSP data files (e.g., `Berlin.tsp`). You must ensure you have tsplib95 installed.
To install tsplib95 run `$ pip install tsplib95` in your terminal. Refer to (https://tsplib95.readthedocs.io/en/stable/pages/installation.html)
 for additional information.


- `numpy` must also be installed. To install open your terminal and run `pip install numpy`. Refer to (https://numpy.org/) for further instructions.


- `matplot` must also be installed. It can be installed in a jupyter notebook by running `!pip install matplotlib` in your notebook.



## Imports required
- `import tsplib95`

- `import random`
- `import numpy as np`
- `import matplotlib.pyplot as plt`
- `import time`

## Loading files
TSP files can be loaded using `tsp.load` like in the following example: ``problem = tsplib95.load('YourFile.tsp')``. In the first cell of the notebook three files have been loaded in two of which have been commented out. Remove ``#`` to load in a particular file.
- ``tsp = tsplib95.load('Berlin.tsp')``

- ``#tsp = tsplib95.load('KroA100.tsp')``

- `` #tsp = tsplib95.load('pr1002.tsp')``

## Parameters
  The main parameters passed as arguments to the function `genetic_algorithm()` are:
- `pop_size`: Size of the population (e.g., 400)

- `max_generations`: Maximum number of generations (e.g., 1000)

- `crossover_prob`: Probability of performing crossover (e.g., 0.4)

- `mutation_prob`: Probability of performing mutation (e.g., 0.2)

- `tournament_size`: Size of the tournament for parent selection (e.g., 3)

- `elite_rate`: Fraction of the population to carry over as elites (e.g., 0.05)

- These parameters can be be initlized also by inputted by prompts by removing the comments for convinience. 

```python
      REMOVE """" TO USE PROMPTS FOR INPUT INSTEAD

       """
      Prompt to enter parameters 
      pop_size = int(input("Enter population size "))
      max_generations = int(input("Enter maximum generations "))
      crossover_prob = float(input("Enter crossover probability "))
      mutation_prob = float(input("Enter mutation probability "))
      tournament_size = int(input("Enter tournament size "))
      elite_rate = float(input("Enter elite rate "))
      """
```
## Crossover and Mutation Parameters
- For the ordered crossover the value of k is defined as`k = int(0.25 * len(nodes))`, the number of genes selected for crossover . This can be changed to experiment,e.g, `k = int(0.15 * len(nodes))`. The probability of either of the crossover operations can also be increased or decreased. If the random float generated when deciding whether crossover occurs is less than a set value than ordered crossover occurs and if not then partially mixed crossover occurs. The probability of one of the crossover operations being used can be altered by varying this set value.
```python
if random.random() < crossover_prob:
                if random.random() < set_value:
                    
                    offspring1, offspring2 = ordered_crossover(parent1, parent2, k) 
                else:
                    offspring1, offspring2 = pmx_crossover(parent1, parent2)
            else:
                
                offspring1, offspring2 = parent1[:], parent2[:]


```

- The probability of either one of the two mutation methods being selected can also be varied. To increase the probability of `inversion_mutation()` being called the value in the `if` statment should be increased closer to 1. This will incidently decrease the probabilty of `shift_mutation()` being called.

   ```python
  import random

   if random.random() < Change_This_Value:
       offspring1 = inversion_mutation(offspring1)
   else:
    offspring1 = shift_mutation(offspring1)
   ```
## Running the algorithm
- To run the algorithm run the cell that calls ``genetic_algorithm()`` passing the appropriate parameters.
     ```python
     best_path, best_fit,fitness_history = genetic_algorithm(pop_size=pop_size,  max_generations=max_generations, crossover_prob=crossover_prob, mutation_prob=mutation_prob, nodes=nodes,tournament_size=tournament_size,elite_rate=elite_rate, dist=dist)
     ```

     This will return the values for the best path found and the fitness associated with it.
