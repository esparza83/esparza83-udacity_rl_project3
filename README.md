[//]: # (Image References)

[image1]: https://user-images.githubusercontent.com/10624937/42135623-e770e354-7d12-11e8-998d-29fc74429ca2.gif "Trained Agent"

# Project 3: Collaboration and Competition  

Udacity Mar 2020  
Pablo Esparza  

### Introduction  

For this project, you will work with the [Tennis](https://github.com/Unity-Technologies/ml-agents/blob/master/docs/Learning-Environment-Examples.md#tennis) environment.

![Trained Agent][image1]

In this environment, two agents control rackets to bounce a ball over a net. If an agent hits the ball over the net, it receives a reward of +0.1.  If an agent lets a ball hit the ground or hits the ball out of bounds, it receives a reward of -0.01.  Thus, the goal of each agent is to keep the ball in play.

The observation space consists of 8 variables corresponding to the position and velocity of the ball and racket. Each agent receives its own, local observation.  Two continuous actions are available, corresponding to movement toward (or away from) the net, and jumping. 

The task is episodic, and in order to solve the environment, your agents must get an average score of +0.5 (over 100 consecutive episodes, after taking the maximum over both agents). Specifically,

- After each episode, we add up the rewards that each agent received (without discounting), to get a score for each agent. This yields 2 (potentially different) scores. We then take the maximum of these 2 scores.
- This yields a single **score** for each episode.

The environment is considered solved, when the average (over 100 episodes) of those **scores** is at least +0.5.

### Instructions

Follow the instructions in `report.ipynb` to get started with training your own agent!  

### Learning algorithm  

The choosen algorihm was Mupti-agent DDPG and some of the tweaked hyperparameters was the batch size, hidden layers, optimization , seed and activations functions.

#### Model  

For the Actor and Critic model file `model.py`,we used a one linear layer followup by a batch layer and two linear layers. For the Critic we used a drop out with value .19. We tested different activation functions like relu, enu, relu6, celu and what it gave us a faster conversion rate was relu.  
For the size of the hidden layers we tested 64, 128, 196, 256, 512 and we got a better result with the 64 size and by using the CPU with got a faster conversion in few episodes.


#### Agent  

For the agent, we tested different mini-batch size: 64, 128, 196, 256, 512 and we got better results with the 512 size.
This type of model is very sensitive to initialization weights, by choosing different seed we got better results, after try and error seed=0 have us a faster conversation rate.  
For the optimizer, we got a better result using pure Adam over simple AdamW.  


#### Result  

After increasing the batch size from 128 to 512 and enable the GPU. We were able to achieve an average score of >= 0.5 in 322 episodes; the time to compute was 18.19 minutes. This project required a lot of hyperparameter tuning; we started using a batch size of 128, 25 minutes to calculate and 2500 episodes.

![image2](https://github.com/esparza83/esparza83-udacity_rl_project3/blob/master/learning.jpg "Rewards plot")
 

#### Ideas for Future Work  

One of the side effects of learning by competition is that agents develop behaviors that are unexpected. In AI theory, this is known as agent autocurricula and represents a first row sit to observing how knowledge develops. [1] Multi-Agent Autocurriculum and Emergent Behavior proposed by Open-AI suggested that by adding more complex situations,"e further provide evidence that multi-agent competition may scale better with increasing environment complexity and leads to behavior that centers around far more human-relevant skills than other self-supervised reinforcement learning methods such as intrinsic motivation."  Will be wort it to try to adapt this technique to the current enviroment.

#### References
[1] EMERGENT TOOL USE FROM MULTI-AGENT AUTOCURRICULA https://arxiv.org/pdf/1909.07528.pdf

