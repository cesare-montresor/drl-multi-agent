[//]: # (Image References)

[scores]: img/scores.png "Scores"


## Learning Algorithm

The algorithm chosen is DDPG, it an actor-critic method.  
The actor network is responsible for chosing actions based on the state and the critic network try to estimate the reward for the given state-action pair.  
DDPG in continuous control is particularly useful as, unlike discrete actions, all the actions are "choose" at every timestep with a continuous value making non-trivial to build a loss function based on these values.  
Instead, the actor network is indirectly trained using gradient ascent on the critic network, reducing the problem of building a loss function to a more classic RL problem of maximize the expected reward.  
The algorithm also leverages the fixed-Q target, double network, soft-updates and experience replay.   


## Plot of Rewards

The currently trained agent passed the goal in about 3341 episodes, however, in the many attempts I must say that this number may vary sensibly.
While the code is provided with a fixed random seed for result replicability, the unity environment is not.
From my observation sometimes happen that the agent has some difficulties in the early training, filling up the replay buffer with poor training examples, which ultimately delay up to 200-300 episodes the solution of the environment and sometimes the trining fails completely making it hard to compare results between modifications.

![Scores][scores]



## Ideas for Future Work

- Layer noise instead of action noise
- Several of the improvements coming from PPO: Gradient clipping, credit assignment and reward normalization.
  

## Other considerations

I've attempted 3 different implementation always using DDPG testing our various hyperparameters:

```DDPG-agent.ipynb``` 1 agents learning both roles (solution delivered)
```DDPG-agent-pre.ipynb``` 1 agent learning both roles with PRE
```MADDPG-agent.ipynb``` 2 agents, using the the full observations of the critic and a single observation for the agent.

For what I've seen the best performing and most consistent have been the standard DDPG, I had even better results with DDPG with PRE (~1200 vs ~3400 ep) but ultimately the training was difficult to replicate with other sessions of training.
As for the MADDPG, the algorithm failed to train.

In all the scenarios where the training worked, it also showed a quite consistent decrease in performance in long training, suggesting a possible overfitting of the network, which, unfortunately dropout shown to decrease the overall performance, probably due to the nature of the problem, my guess is that setting activations to 0 continuous problems may lead to the wrong interpretation.
Other forms of regularisations should be considered, including batch normalisation, L2 or simply trying to reduce the size of the network for the given problem.

## Training history


```
Episode 100	 Score: -0.00 	Average Score: 0.01
Episode 200	 Score: -0.00 	Average Score: 0.01
Episode 300	 Score: 0.10 	Average Score: 0.021
Episode 400	 Score: 0.05 	Average Score: 0.011
Episode 500	 Score: -0.00 	Average Score: 0.01
Episode 600	 Score: 0.05 	Average Score: 0.022
Episode 700	 Score: 0.05 	Average Score: 0.022
Episode 800	 Score: -0.00 	Average Score: 0.02
Episode 900	 Score: 0.05 	Average Score: 0.011
Episode 1000	 Score: -0.00 	Average Score: 0.02
Episode 1100	 Score: 0.05 	Average Score: 0.011
Episode 1200	 Score: -0.00 	Average Score: 0.02
Episode 1300	 Score: 0.05 	Average Score: 0.022
Episode 1400	 Score: -0.00 	Average Score: 0.02
Episode 1500	 Score: -0.00 	Average Score: 0.02
Episode 1600	 Score: 0.05 	Average Score: 0.033
Episode 1700	 Score: -0.00 	Average Score: 0.03
Episode 1800	 Score: 0.05 	Average Score: 0.033
Episode 1900	 Score: -0.00 	Average Score: 0.02
Episode 2000	 Score: 0.05 	Average Score: 0.033
Episode 2100	 Score: -0.00 	Average Score: 0.04
Episode 2200	 Score: 0.10 	Average Score: 0.066
Episode 2300	 Score: -0.00 	Average Score: 0.08
Episode 2400	 Score: 0.10 	Average Score: 0.088
Episode 2500	 Score: 0.15 	Average Score: 0.109
Episode 2600	 Score: -0.00 	Average Score: 0.12
Episode 2700	 Score: 0.05 	Average Score: 0.198
Episode 2800	 Score: 0.10 	Average Score: 0.222
Episode 2900	 Score: 0.30 	Average Score: 0.222
Episode 3000	 Score: 0.25 	Average Score: 0.235
Episode 3100	 Score: 0.85 	Average Score: 0.309
Episode 3200	 Score: 0.25 	Average Score: 0.324
Episode 3300	 Score: 0.35 	Average Score: 0.433
Episode 3341	 Score: 0.90 	Average Score: 0.502
Environment solved in 3341 episodes!	Average Score: 0.500
Episode 3342	 Score: 0.35 	Average Score: 0.50
Environment solved in 3342 episodes!	Average Score: 0.501
Episode 3345	 Score: 1.25 	Average Score: 0.51
Environment solved in 3345 episodes!	Average Score: 0.510
Episode 3346	 Score: -0.00 	Average Score: 0.51
Environment solved in 3346 episodes!	Average Score: 0.506
Episode 3347	 Score: 0.60 	Average Score: 0.51
Environment solved in 3347 episodes!	Average Score: 0.506
Episode 3348	 Score: -0.00 	Average Score: 0.50
Environment solved in 3348 episodes!	Average Score: 0.501
Episode 3349	 Score: 0.60 	Average Score: 0.51
Environment solved in 3349 episodes!	Average Score: 0.506
Episode 3350	 Score: 0.40 	Average Score: 0.51
Environment solved in 3350 episodes!	Average Score: 0.509
Episode 3351	 Score: 0.30 	Average Score: 0.51
Environment solved in 3351 episodes!	Average Score: 0.512
Episode 3352	 Score: 0.20 	Average Score: 0.51
Environment solved in 3352 episodes!	Average Score: 0.512
Episode 3353	 Score: 1.25 	Average Score: 0.52
Environment solved in 3353 episodes!	Average Score: 0.522
Episode 3354	 Score: 2.60 	Average Score: 0.55
Environment solved in 3354 episodes!	Average Score: 0.546
Episode 3355	 Score: 0.20 	Average Score: 0.55
Environment solved in 3355 episodes!	Average Score: 0.545
Episode 3356	 Score: 0.40 	Average Score: 0.54
Environment solved in 3356 episodes!	Average Score: 0.539
Episode 3357	 Score: 1.80 	Average Score: 0.56
Environment solved in 3357 episodes!	Average Score: 0.556
Episode 3358	 Score: -0.00 	Average Score: 0.56
Environment solved in 3358 episodes!	Average Score: 0.556
Episode 3359	 Score: 0.55 	Average Score: 0.56
Environment solved in 3359 episodes!	Average Score: 0.561
Episode 3360	 Score: 0.10 	Average Score: 0.55
Environment solved in 3360 episodes!	Average Score: 0.555
Episode 3361	 Score: 1.75 	Average Score: 0.57
Environment solved in 3361 episodes!	Average Score: 0.572
Episode 3362	 Score: 0.15 	Average Score: 0.57
Environment solved in 3362 episodes!	Average Score: 0.572
Episode 3363	 Score: 0.35 	Average Score: 0.57
Environment solved in 3363 episodes!	Average Score: 0.574
Episode 3364	 Score: 0.75 	Average Score: 0.58
Environment solved in 3364 episodes!	Average Score: 0.578
Episode 3365	 Score: 0.45 	Average Score: 0.58
Environment solved in 3365 episodes!	Average Score: 0.582
Episode 3366	 Score: -0.00 	Average Score: 0.58
Environment solved in 3366 episodes!	Average Score: 0.581
Episode 3367	 Score: 0.45 	Average Score: 0.58
Environment solved in 3367 episodes!	Average Score: 0.579
Episode 3368	 Score: 0.75 	Average Score: 0.59
Environment solved in 3368 episodes!	Average Score: 0.586
Episode 3369	 Score: 0.80 	Average Score: 0.59
Environment solved in 3369 episodes!	Average Score: 0.590
Episode 3370	 Score: 1.80 	Average Score: 0.60
Environment solved in 3370 episodes!	Average Score: 0.605
Episode 3371	 Score: -0.00 	Average Score: 0.60
Environment solved in 3371 episodes!	Average Score: 0.602
Episode 3372	 Score: 0.15 	Average Score: 0.60
Environment solved in 3372 episodes!	Average Score: 0.596
Episode 3373	 Score: 0.10 	Average Score: 0.60
Environment solved in 3373 episodes!	Average Score: 0.596
Episode 3374	 Score: 0.20 	Average Score: 0.60
Environment solved in 3374 episodes!	Average Score: 0.596
Episode 3375	 Score: 1.50 	Average Score: 0.61
Environment solved in 3375 episodes!	Average Score: 0.607
Episode 3376	 Score: 0.45 	Average Score: 0.61
Environment solved in 3376 episodes!	Average Score: 0.609
Episode 3377	 Score: 0.45 	Average Score: 0.61
Environment solved in 3377 episodes!	Average Score: 0.606
Episode 3378	 Score: 0.10 	Average Score: 0.59
Environment solved in 3378 episodes!	Average Score: 0.592
Episode 3379	 Score: -0.00 	Average Score: 0.57
Environment solved in 3379 episodes!	Average Score: 0.574
Episode 3380	 Score: 0.80 	Average Score: 0.57
Environment solved in 3380 episodes!	Average Score: 0.572
Episode 3381	 Score: 0.65 	Average Score: 0.57
Environment solved in 3381 episodes!	Average Score: 0.572
Episode 3382	 Score: 2.55 	Average Score: 0.60
Environment solved in 3382 episodes!	Average Score: 0.595
Episode 3383	 Score: 0.45 	Average Score: 0.60
Environment solved in 3383 episodes!	Average Score: 0.599
Episode 3384	 Score: 0.85 	Average Score: 0.61
Environment solved in 3384 episodes!	Average Score: 0.607
Episode 3385	 Score: 0.35 	Average Score: 0.61
Environment solved in 3385 episodes!	Average Score: 0.609
Episode 3386	 Score: 1.25 	Average Score: 0.61
Environment solved in 3386 episodes!	Average Score: 0.611
Episode 3387	 Score: 0.40 	Average Score: 0.61
Environment solved in 3387 episodes!	Average Score: 0.613
Episode 3388	 Score: 0.75 	Average Score: 0.62
Environment solved in 3388 episodes!	Average Score: 0.619
Episode 3389	 Score: 0.10 	Average Score: 0.61
Environment solved in 3389 episodes!	Average Score: 0.605
Episode 3390	 Score: 0.30 	Average Score: 0.61
Environment solved in 3390 episodes!	Average Score: 0.607
Episode 3391	 Score: 0.10 	Average Score: 0.61
Environment solved in 3391 episodes!	Average Score: 0.608
Episode 3392	 Score: 0.35 	Average Score: 0.61
Environment solved in 3392 episodes!	Average Score: 0.610
Episode 3393	 Score: 0.95 	Average Score: 0.62
Environment solved in 3393 episodes!	Average Score: 0.618
Episode 3394	 Score: -0.00 	Average Score: 0.62
Environment solved in 3394 episodes!	Average Score: 0.617
Episode 3395	 Score: 0.75 	Average Score: 0.62
Environment solved in 3395 episodes!	Average Score: 0.620
Episode 3396	 Score: 0.10 	Average Score: 0.62
Environment solved in 3396 episodes!	Average Score: 0.619
Episode 3397	 Score: 0.30 	Average Score: 0.62
Environment solved in 3397 episodes!	Average Score: 0.620
Episode 3398	 Score: 0.15 	Average Score: 0.61
Environment solved in 3398 episodes!	Average Score: 0.608
Episode 3399	 Score: -0.00 	Average Score: 0.60
Environment solved in 3399 episodes!	Average Score: 0.605
Episode 3400	 Score: 0.20 	Average Score: 0.60

Environment solved in 3400 episodes!	Average Score: 0.603
Episode 3401	 Score: 0.10 	Average Score: 0.60
Environment solved in 3401 episodes!	Average Score: 0.599
Episode 3402	 Score: 0.10 	Average Score: 0.59
Environment solved in 3402 episodes!	Average Score: 0.589
Episode 3403	 Score: -0.00 	Average Score: 0.59
Environment solved in 3403 episodes!	Average Score: 0.586
Episode 3404	 Score: 0.05 	Average Score: 0.59
Environment solved in 3404 episodes!	Average Score: 0.587
Episode 3405	 Score: 0.30 	Average Score: 0.58
Environment solved in 3405 episodes!	Average Score: 0.584

Episode 3406	 Score: -0.00 	Average Score: 0.58
Environment solved in 3406 episodes!	Average Score: 0.583
Episode 3407	 Score: 0.20 	Average Score: 0.57
Environment solved in 3407 episodes!	Average Score: 0.573
Episode 3408	 Score: -0.00 	Average Score: 0.57
Environment solved in 3408 episodes!	Average Score: 0.570
Episode 3409	 Score: 0.10 	Average Score: 0.57
Environment solved in 3409 episodes!	Average Score: 0.569
Episode 3410	 Score: 0.20 	Average Score: 0.56
Environment solved in 3410 episodes!	Average Score: 0.565
Episode 3411	 Score: 0.10 	Average Score: 0.56
Environment solved in 3411 episodes!	Average Score: 0.558
Episode 3412	 Score: 0.35 	Average Score: 0.55
Environment solved in 3412 episodes!	Average Score: 0.549
Episode 3413	 Score: 0.05 	Average Score: 0.53
Environment solved in 3413 episodes!	Average Score: 0.532
Episode 3414	 Score: 1.10 	Average Score: 0.54
Environment solved in 3414 episodes!	Average Score: 0.540
Episode 3415	 Score: 0.30 	Average Score: 0.54
Environment solved in 3415 episodes!	Average Score: 0.541
Episode 3416	 Score: 0.60 	Average Score: 0.54
Environment solved in 3416 episodes!	Average Score: 0.540
Episode 3417	 Score: 0.10 	Average Score: 0.54
Environment solved in 3417 episodes!	Average Score: 0.537
Episode 3418	 Score: 0.10 	Average Score: 0.53
Environment solved in 3418 episodes!	Average Score: 0.535
Episode 3419	 Score: 0.70 	Average Score: 0.53
Environment solved in 3419 episodes!	Average Score: 0.534
Episode 3420	 Score: 0.65 	Average Score: 0.54
Environment solved in 3420 episodes!	Average Score: 0.539
Episode 3421	 Score: 0.95 	Average Score: 0.55
Environment solved in 3421 episodes!	Average Score: 0.545
Episode 3422	 Score: -0.00 	Average Score: 0.54
Environment solved in 3422 episodes!	Average Score: 0.540
Episode 3423	 Score: 1.40 	Average Score: 0.54
Environment solved in 3423 episodes!	Average Score: 0.545
Episode 3424	 Score: 1.40 	Average Score: 0.55
Environment solved in 3424 episodes!	Average Score: 0.549
Episode 3425	 Score: 0.10 	Average Score: 0.54
Environment solved in 3425 episodes!	Average Score: 0.541
Episode 3426	 Score: 0.10 	Average Score: 0.54
Environment solved in 3426 episodes!	Average Score: 0.542
Episode 3427	 Score: 0.10 	Average Score: 0.54
Environment solved in 3427 episodes!	Average Score: 0.540
Episode 3428	 Score: -0.00 	Average Score: 0.54
Environment solved in 3428 episodes!	Average Score: 0.536
Episode 3429	 Score: 0.50 	Average Score: 0.54
Environment solved in 3429 episodes!	Average Score: 0.536
Episode 3430	 Score: -0.00 	Average Score: 0.53
Environment solved in 3430 episodes!	Average Score: 0.534
Episode 3431	 Score: 0.20 	Average Score: 0.53
Environment solved in 3431 episodes!	Average Score: 0.527
Episode 3432	 Score: -0.00 	Average Score: 0.51
Environment solved in 3432 episodes!	Average Score: 0.510
Episode 3433	 Score: 0.05 	Average Score: 0.51
Environment solved in 3433 episodes!	Average Score: 0.510
Episode 3434	 Score: 0.50 	Average Score: 0.51
Environment solved in 3434 episodes!	Average Score: 0.514
Episode 3435	 Score: 0.05 	Average Score: 0.51
Environment solved in 3435 episodes!	Average Score: 0.506
Episode 3500	 Score: -0.00 	Average Score: 0.35
Episode 3600	 Score: 0.10 	Average Score: 0.334
Episode 3700	 Score: 0.15 	Average Score: 0.299
Episode 3800	 Score: 0.05 	Average Score: 0.245
Episode 3900	 Score: 1.10 	Average Score: 0.265
Episode 4000	 Score: 0.10 	Average Score: 0.244
Episode 4100	 Score: -0.00 	Average Score: 0.22
Episode 4200	 Score: 0.10 	Average Score: 0.311
Episode 4300	 Score: -0.00 	Average Score: 0.25
Episode 4400	 Score: 0.80 	Average Score: 0.297
Episode 4500	 Score: 0.20 	Average Score: 0.299
Episode 4600	 Score: 0.05 	Average Score: 0.221
Episode 4700	 Score: 0.20 	Average Score: 0.201
Episode 4800	 Score: 0.10 	Average Score: 0.221
Episode 4900	 Score: 0.50 	Average Score: 0.189
Episode 5000	 Score: 0.20 	Average Score: 0.134
Episode 5100	 Score: 0.15 	Average Score: 0.166
Episode 5200	 Score: -0.00 	Average Score: 0.12
Episode 5300	 Score: 0.05 	Average Score: 0.133
Episode 5400	 Score: 0.10 	Average Score: 0.187
Episode 5500	 Score: -0.00 	Average Score: 0.18
Episode 5600	 Score: 0.15 	Average Score: 0.199
Episode 5700	 Score: 0.05 	Average Score: 0.200
Episode 5800	 Score: 0.30 	Average Score: 0.177
Episode 5900	 Score: 0.34 	Average Score: 0.244
Episode 6000	 Score: 0.20 	Average Score: 0.188
Episode 6100	 Score: 0.10 	Average Score: 0.188
Episode 6200	 Score: -0.00 	Average Score: 0.27
Episode 6300	 Score: 0.10 	Average Score: 0.244
Episode 6400	 Score: 0.25 	Average Score: 0.344
Episode 6500	 Score: 0.10 	Average Score: 0.266
Episode 6600	 Score: 0.10 	Average Score: 0.256
Episode 6700	 Score: 0.10 	Average Score: 0.258
Episode 6800	 Score: 0.15 	Average Score: 0.200
Episode 6900	 Score: 0.05 	Average Score: 0.166
Episode 7000	 Score: 0.15 	Average Score: 0.177
Episode 7100	 Score: 0.05 	Average Score: 0.100
Episode 7200	 Score: 0.05 	Average Score: 0.133
Episode 7300	 Score: 0.15 	Average Score: 0.188
Episode 7400	 Score: -0.00 	Average Score: 0.14
Episode 7500	 Score: -0.00 	Average Score: 0.13
Episode 7600	 Score: 0.15 	Average Score: 0.155
Episode 7700	 Score: 0.05 	Average Score: 0.122
Episode 7800	 Score: 0.20 	Average Score: 0.111
Episode 7900	 Score: -0.00 	Average Score: 0.18
Episode 8000	 Score: 0.25 	Average Score: 0.166
Episode 8100	 Score: -0.00 	Average Score: 0.17
Episode 8200	 Score: 0.10 	Average Score: 0.155
Episode 8300	 Score: 0.15 	Average Score: 0.111
Episode 8400	 Score: 0.20 	Average Score: 0.207
Episode 8500	 Score: -0.00 	Average Score: 0.16
Episode 8600	 Score: 1.35 	Average Score: 0.218
Episode 8700	 Score: 0.05 	Average Score: 0.190
Episode 8800	 Score: 0.05 	Average Score: 0.198
Episode 8900	 Score: 0.05 	Average Score: 0.210
Episode 9000	 Score: 0.45 	Average Score: 0.244
Episode 9100	 Score: 0.30 	Average Score: 0.144
Episode 9200	 Score: -0.00 	Average Score: 0.14
Episode 9300	 Score: 0.60 	Average Score: 0.188
Episode 9400	 Score: 0.45 	Average Score: 0.219
Episode 9500	 Score: 0.50 	Average Score: 0.167
Episode 9600	 Score: 0.05 	Average Score: 0.223
Episode 9700	 Score: 0.10 	Average Score: 0.210
Episode 9800	 Score: 0.35 	Average Score: 0.166
Episode 9900	 Score: 0.05 	Average Score: 0.212
Episode 10000	 Score: 0.05 	Average Score: 0.15

```
