# Population-based training

Based on the DeepMind paper: https://arxiv.org/abs/1711.09846

Blog post: https://deepmind.com/blog/population-based-training-neural-networks/

# Contribution

Look at two different ways to implement PBT as a reusable algorithm.

The second version that implements it as a pure advisor function seems to be
the more flexible one.

The first iteration contains code to recreate Figure 2 from the paper.
I had to change the initial hyperparameters a bit to break symmetries and I had
to modify the proxy function to not allow negative hyperparameters (otherwise,
it runs off into infinity if it perturbs the hyperparameters to be negative by 
accident).

# Critique of the paper

General feel after playing around with the idea is that it describes a nice
heuristic. However, you are also replacing a set of more tangible hyperparameters
by meta-hyperparameters that control this heuristic: 

* how to determine whether a worker is ready;
* how to perturb hyperparameters during exploration; and,
* how to determine whether a worker is underperforming or not.

Moreover, one could use different strategies during exploitation, like selecting
one of the top5 workers instead of the top1 worker during exploration, all the 
way to simulated annealing.

The main contribution of PBT (as mentioned on reddit) seems to be that 
exploration means copying of the weights and continuing training from then on.
This saves time but this also means that it will be even harder to ensure
reproducibility. Now, one also almost has to save a history of the exploration 
steps to be able to explain how to get to a certain result.
 