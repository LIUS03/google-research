# Concept MARL
This repo implements Concept Bottleneck Policies, as described in
Grupen et al. [1]. The algorithm extends the MultiAgent-PPO algorithm from
in [Acme](https://github.com/deepmind/acme), adding a concept loss term
to the PPO objective. Custom policy networks that incorporate the concept
bottleneck architecture are provided in `helpers.py`.

This repo also includes custom implementations of the following environments
from [DeepMind Melting Pot](https://github.com/deepmind/meltingpot):
1. Collaborative Cooking

Each environment is extended to support concept extraction, and miniature
versions of the original collaborative cooking environments are also provided.
The custom concept bottleneck policy networks include an encoder that processes
Melting Pot's default multi-modal observations (RGB, position, orientation).

This repo also provides the following wrappers which are used for training
concept bottleneck policies:
1.`meltingpot_wrapper.py`: Converts Melting Pot environment specs to dm_env
specs used by Acme.
2.`ma_concept_extraction_wrapper.py`: Parses concept values for each agent from
environment observations using a common prefix. Concept values parsed here are
used to compute the concept loss term in `concept_ppo/learning.py`.
3.`meltingpot_cooking_dense_rewards_wrapper.py`: Implements pseudo-rewards
specific to the collaborative cooking task.

## Training
To train Concept PPO agents in the Melting Pot collaborative cooking environment, run:
```
python -m experiments/run_meltingpot.py --env_name='cooking_basic' \
--checkpoint_dir=/tmp/cooking_basic
```

## Other Notes
This project requires manual installation of DeepMind Melting Pot. Installation
instructions can be found [here](https://github.com/deepmind/meltingpot).

## References
[1] N. Grupen, N. Jaques, B. Kim, S. Omidshafiei, "Concept-based Understanding of
Emergent Multi-Agent Behavior, NeuIPS Deep RL Workshop 2022 (paper link coming soon).
