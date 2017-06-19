# Behavioral Cloning

## Main Idea

This runs Behavioral Cloning (BC) on MuJoCo environments. Specifically:

- The expert is TRPO and provided from Jonathan Ho (see below).
- Dataset consists of inputs (states=s) to labels (actions=a). They're
  continuous, so minimize L2 loss.
- Batch size of 128 state/action pairs each iteration.
- Trained with Adam, with a step size of 1e-3.
- Data is split into 70% training, 30% validation.
- The BC network we use is the one which performed best on the validation set.
- The neural network (from TensorFlow) is fully connected and has two hidden
  layers of 100 units each with hyperbolic tangent non-linearities.


## Running the Code

To run BC, there are several steps:

- (If needed) generate expert data. Run

  ```
  ./bash_scripts/gen_exp_data.sh
  ```

  which will run and save expert trajectories in numpy arrays. They're not saved
  in the repository (ask if you want my version). By default, the number of
  trajectories is saved into the file name by default and matches the values in
  [Generative Adversarial Imitation Learning paper][1] (see Table 1). 
  
- **TODO running the code TODO**

- To plot the code, it's simple: `python plot_bc.py`. No command line arguments!


Other stuff if you're interested:

- The expert performance that I'm seeing is roughly similar to what's reported
  in the paper, with the exception of the Walker environment, but I may be
  running a different version of it. See the output in `logs/gen_exp_data.text`
  for details.

- The `bash_scripts` directory also contains a file called `demo.bash`, which
  you can use to visualize expert trajectories, just for fun.


# Results

Note that ant, halfcheetah, hopper, and walker use 4, 11, 18, and 25 expert
rollouts since that follows the GAIL paper. The humanoid environment uses 80,
160, and 240 expert trajectories.

## Ant-v1

![ant](figures/Ant-v1.png?raw=true)

## HalfCheetah-v1

![halfcheetah](figures/HalfCheetah-v1.png?raw=true)

## Hopper-v1

![hopper](figures/Hopper-v1.png?raw=true)

## Walker2d-v1

![walker2d](figures/Walker2d-v1.png?raw=true)


# Original Notes from Berkeley

This started from UC Berkeley's Deep Reinforcement Learning class. Here's their
information:

> Dependencies: TensorFlow, MuJoCo version 1.31, OpenAI Gym
> 
> The only file that you need to look at is `run_expert.py`, which is code to
> load up an expert policy, run a specified number of roll-outs, and save out
> data.
> 
> In `experts/`, the provided expert policies are:
> * Ant-v1.pkl
> * HalfCheetah-v1.pkl
> * Hopper-v1.pkl
> * Humanoid-v1.pkl
> * Reacher-v1.pkl
> * Walker2d-v1.pkl
> 
> The name of the pickle file corresponds to the name of the gym environment.

[1]:https://arxiv.org/abs/1606.03476