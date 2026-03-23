# Assignment 2 — Genetic Algorithm: Knapsack Problem
## Observation Report

**Student Name  :** S. Ravi Ratna  
**Student ID    :** 2310040132
**Date Submitted:** 23/03/2026 

---

## How to Submit

1. Run each experiment following the instructions below
2. Fill in every answer box — do not leave placeholders
3. Make sure the `plots/` folder contains all required images
4. Commit this README and the `plots/` folder to your GitHub repo

---

## Before You Begin — Read the Code

Open `ga_knapsack.py` and read through it. Then answer these questions.

**Q1. What does the `fitness()` function return? Why does an overweight solution score 0?**

The fitness() function returns the total value of the packed items if the total weight does not exceed the maximum weight limit of 15 kg. If the total weight exceeds the limit, it returns 0. An overweight solution scores 0 to heavily penalize invalid solutions, ensuring that only feasible knapsacks are considered optimal and preventing the algorithm from favoring high-value but overweight combinations.
```

**Q2. What does `tournament_select()` do? Why are higher-fitness individuals more likely to be chosen?**

The tournament_select() function selects the best individual from a random sample of k candidates from the population. Higher-fitness individuals are more likely to be chosen because the function uses the max() function with the fitness values as the key, so it always picks the candidate with the highest fitness score among the sampled ones, giving better solutions a higher probability of selection.
```

**Q3. Look at the `run_ga()` loop. Find this line:**
```python
next_gen = [best_chromosome[:]]
```
**What is this doing? Why is it important to always keep the best solution?**

This line implements elitism by ensuring the best chromosome found so far is always carried over to the next generation unchanged. It is important to always keep the best solution to prevent the loss of high-quality individuals through crossover or mutation, guaranteeing that the algorithm never degrades the best solution and maintains progress towards optimal fitness.

---

## Experiment 1 — Baseline Run

**Instructions:** Run the program without changing anything.
```bash
python ga_knapsack.py
```

**Fill in this table:**

| Metric | Your result |
|--------|-------------|
| Number of generations | 50 |
| Best value at generation 1 | 60 |
| Final best value | 77 |
| Total weight of best solution (kg) | 14.4 |
| Is solution valid (Yes / No) | Yes |

**Copy the printed packing list here:**
```
  Best Packing List
--------------------------------------
  + Water bottle
  + First aid kit
  + Sleeping bag
  + Torch
  + Energy bars (x6)
  + Rain jacket
  + Map & compass
  + Cooking stove
  + Rope (10 m)
  + Sunscreen
  + Power bank
--------------------------------------
  Weight : 14.4 / 15.0 kg
  Value  : 77
  Valid  : Yes
```

**Look at `plots/experiment_1.png` and describe what you see (2–3 sentences).**  
*Where does the biggest improvement happen? Does the curve flatten at some point?*
The plot shows the best fitness value increasing over generations, starting at 60 in generation 1. The biggest improvement occurs in the early generations, where the value rises rapidly from 60 to around 77. The curve then flattens out after about 10-15 generations, indicating that the algorithm converges to the optimal solution without further significant gains.

---

## Experiment 2 — Effect of Mutation Rate

**Instructions:** In `ga_knapsack.py`, find the `# EXPERIMENT 2` block in `__main__`.  
Copy it three times and run with `mutation_rate` = **0.01**, **0.05**, and **0.30**.  
Save plots as `experiment_2a.png`, `experiment_2b.png`, `experiment_2c.png`.

**Results table:**

| mutation_rate | Final best value | Weight (kg) | Valid? | Shape of curve |
|--------------|-----------------|-------------|--------|----------------|
| 0.01         | 75              | 14.9        | Yes    | Slow initial improvement, plateaus early |
| 0.05         | 77              | 14.4        | Yes    | Steady improvement, converges well |
| 0.30         | 78              | 14.1        | Yes    | Erratic with fluctuations, finds high value |

**Compare the three plots. What happens when mutation is too low? Too high? (3–4 sentences)**  
*Hint: Too low = no diversity, may get stuck. Too high = random search. What is the sweet spot?*
When mutation rate is too low (0.01), the algorithm lacks diversity, leading to slow improvement and getting stuck at suboptimal solutions due to insufficient exploration. When mutation rate is too high (0.30), it introduces too much randomness, causing erratic behavior that can disrupt good solutions but sometimes finds better ones by chance. The sweet spot appears to be around 0.05, where there's balanced exploration and exploitation, allowing steady convergence to high-quality solutions without excessive randomness.
```

**Which mutation_rate gave the best result? Why do you think that is?**
0.30 gave the best result with a value of 78. This is likely because the higher mutation rate allowed for more exploration of the solution space, occasionally producing beneficial random changes that led to a better combination, despite the increased risk of disrupting good solutions.

---

## Summary

**Complete this table with your best result from each experiment:**

| Experiment | Key setting | Final value | Main finding in one sentence |
|------------|-------------|-------------|------------------------------|
| 1 — Baseline | mutation_rate = 0.05 | 77 | The baseline GA converges to a good solution with balanced parameters. |
| 2 — Mutation rate | mutation_rate = 0.30 | 78 | Higher mutation rates can find better solutions through increased exploration. |

**In your own words — what is the most important thing you learned about Genetic Algorithms from these experiments? (3–5 sentences)**
Genetic algorithms are powerful for optimization problems like the knapsack problem, using selection, crossover, and mutation to evolve solutions over generations. The importance of balancing exploration and exploitation was evident, as mutation rate critically affects performance—too low leads to stagnation, too high to randomness. Elitism ensures the best solutions are preserved, preventing regression, and the convergence plots show how GAs can efficiently find near-optimal solutions in constrained spaces.

---

## Submission Checklist

- [ ] Student name and ID filled in
- [ ] Q1, Q2, Q3 answered
- [ ] Experiment 1: table filled, packing list pasted, plot observation written
- [ ] Experiment 2: results table filled (3 rows), observation and answer written
- [ ] Summary table completed and reflection written
- [ ] `plots/` contains: `experiment_1.png`, `experiment_2a.png`, `experiment_2b.png`, `experiment_2c.png`
