# Real-Time Reinforcement Learning

This repo contains


### Getting Started
This repo can be pip-installed via
```bash
pip install git+https://github.com/rmst/rtrl.git
```

To train an RTAC agent on the basic `Pendulum-v0` task run
```bash
python -m rtrl run rtrl:RtacTraining Env.id=Pendulum-v0
```



### Mujoco Experiments
To install Mujoco you follow the instructions at [openai/gym](https://github.com/openai/gym) or have a look at [`docker/gym/Dockerfile`](github.com/rmst/rtrl/blob/master/docker/gym/Dockerfile).

To train an RTAC agent on `HalfCheetah-v2` run
```bash
python -m rtrl run rtrl:RtacTraining Env.id=HalfCheetah-v2
```

To train a SAC agent on `Ant-v2` with a real-time wrapper (i.e. RTMDP in the paper) run
```bash
python - rtrl run rtrl:SacTraining Env.id=Ant-v2 Env.real_time=True
```

### Avenue Experiments
Avenue can be pip-installed via
```bash
pip install git+https://github.com/elementai/avenue.git
```

To train an RTAC agent to drive on an empty road run
```bash
python -m rtrl run rtrl:RtacAvenueTraining Env.id=RaceSolo-v0
```
Note that this requires a lot of resources, especially memory (16GB+).


### Storing Stats
`python -m rtrl run` just prints stats to stdout. To save stats as pickled pandas dataframes use `python -m rtrl run-fs my-rtrl-experiment rtrl:RtacTraining Env.id=Pendulum-v0` instead. Stats are generated and printed every `round` but only saved to disk every `epoch`.

### Checkpointing
This repo supports checkpointing. Every `epoch` the whole run object (e.g. instances of `rtrl.training:Training`) is pickled to disk and reloaded. This is to ensure reproducibilty.

You can manually load and inspect pickled run instances with the standard `picke:load` or do for convenience use `rtrl:load`. For example, to look at the first transition in a SAC agent's replay memory run
```python
import rtrl
run = rtrl.load('rtrl-checkpoints/test')
print(run.agent.memory.memory[0])
``` 