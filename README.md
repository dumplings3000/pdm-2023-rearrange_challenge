## Installation

```bash
# Ensure the latest submodules
git submodule update --init --recursive

# Activate the conda env
conda activate habitat
conda install cmake=3.14.0 patchelf ninja

# Install habitat-lab
cd habitat-lab && pip install -r requirements.txt && python setup.py develop && cd ..
# Install requirements
pip install -r requirements.txt
# Install habitat manipulation
python setup.py develop
# Post-installation
echo "export MAGNUM_LOG=quiet HABITAT_SIM_LOG=quiet" >> ~/.bashrc
```
---
## Evaluation

### Evaluate a sub-task

```bash
# Evaluate the latest checkpoint of a skill saved at "data/results/rearrange/skills/tidy_house/pick_v1_joint_SCR"
python mobile_manipulation/run_ppo.py --cfg configs/rearrange/skills/tidy_house/pick_v1_joint_SCR.yaml --run-type eval
# Evaluate the latest checkpoint of a skill saved at "data/results/rearrange/skills/tidy_house/pick_v1_joint_SCR/seed=100"
python mobile_manipulation/run_ppo.py --cfg configs/rearrange/skills/tidy_house/pick_v1_joint_SCR.yaml --run-type eval --run-type eval PREFIX seed=100
```
### Evaluate a HAB (Home Assistant Benchmark) task

```bash
# Interactively visualize results
python mobile_manipulation/eval_composite.py --cfg configs/rearrange/composite/tidy_house/mr.yaml --viewer --render-info
# Save results
# "--no-rgb" can be passed to the script to accelerate if rgb is not used.
python mobile_manipulation/eval_composite.py --cfg configs/rearrange/composite/tidy_house/mr.yaml --save-log
# Save videos
python mobile_manipulation/eval_composite.py --cfg configs/rearrange/composite/tidy_house/mr.yaml --save-video all
```

---

## Training

Train an individual skill (e.g., *Pick* for TidyHouse):

```bash
# The result will be saved at "data/results/rearrange/skills/tidy_house/pick_v1_joint_SCR".
python mobile_manipulation/run_ppo.py --cfg configs/rearrange/skills/tidy_house/pick_v1_joint_SCR.yaml --run-type train
# Specify a prefix and a random seed for the experiment.
# The result will be saved at "data/results/rearrange/skills/tidy_house/pick_v1_joint_SCR/seed=101" 
python mobile_manipulation/run_ppo.py --cfg configs/rearrange/skills/tidy_house/pick_v1_joint_SCR.yaml --run-type train PREFIX seed=101 TASK_CONFIG.SEED 101
```

## Acknowledgments

This repository is inspired by [Habitat Lab](https://github.com/facebookresearch/habitat-lab) for RL environments and PPO implementation. We would also like to thank [Andrew Szot](https://www.andrewszot.com/) and [Alexander Clegg](https://scholar.google.com/citations?user=p463opcAAAAJ&hl=en) for their help in using Habitat 2.0.
