# MEEV-LN:

This repository is the PyTorch implementation of [MEEV-LN].

[MEEV-LN: Multi-Task Evaluation Framework for Zero-Shot Vision-and-Language Navigation]
</br>
Haoze Zhao, 
Liang Ma,
Yuyang Liu


--------



## Overview
MEEV-LN: provides four tasks: 1) goal-conditioned navigation given a specific object category (e.g., "fork"); 2) goal-conditioned navigation given simple instructions (e.g., "Search for and move towards a tennis ball"); 3) step-by-step instruction following; 4) finding abstract object based on high-level instruction (e.g., "I am thirsty"). The earlier version of our simulator covers three high-quality scenes: cafe, restaurant, and nursing house.

![scene](./docs/scenes.png)

![task](./docs/tasks.png)


## Installing Dependencies
- Installing the simulator following [here](https://mligg23.github.io/MEEV-LN:-Site/Simulation%20Environment%20API.html).

- Installing [GLIP](https://github.com/microsoft/GLIP).

- Installing [Grounded-SAM](https://github.com/IDEA-Research/Grounded-Segment-Anything).


## Setup
Clone the repository and install other requirements:
```
git clone https://github.com/liangcici/MEEV-LN:.git
cd MEEV-LN:/
pip install -r requirements.txt
```

### Setting up the dataset
- Downloading original datasets from [here](https://drive.google.com/drive/folders/1khtQ9zRfWQX0WtsMWq3NkRNMvjH0JiZi).

- Generate data for ObjectNav (goal-conditioned navigation given a specific object category).
```
python data_preprocess/gen_objectnav.py --map_id 3
```
map_id indicates specific scene: `{3: Starbucks; 4: TG; 5: NursingRoom}`.


## Usage
The implementation is based on frontier-based exploration (FBE). Exploration with commonsense knowledge as in our paper is based on [ESC](https://sites.google.com/ucsc.edu/escnav/home), which is not allowed to be released. `dataset/objectnav/*.npy` are knowledge extracted from LLMs, and can be used to reproduce exploration with commonsense knowledge.

Run models with FBE:

- For ObjectNav:
```
python zero_shot_eval.py --sem_seg_model_type glip --map_id 3
```


## Related Projects
- The Semantic Mapping module is based on [SemExp](https://github.com/devendrachaplot/Object-Goal-Navigation).


## To-Do List
- [x] Added **more walker states**.
- [x] Added **walker control interface**.
- [ ] Provide **more classes of generative objects**.
- [ ] **Construct complex tasks involving combined navigation and grasping.**
- [ ] **10+ scenes** are under construction and will be updated successively in the future.
- [ ] Generate high-quality instruction-ground truth pairs for the newly constructed scenes.
- [ ] Continue to update the simulator's **physics engine effects** to achieve more **realistic dexterous hand-grabbing effects**
- [ ] Adding **more interactive properties to objects in the environment**, such as a coffee machine that can be controlled to make coffee.



## Citation
```
@article{liang2023mo,
  title={MEEV-LN:: A Multi-Task Benchmark for Open-set Zero-Shot Vision-and-Language Navigation},
  author={Liang, Xiwen and Ma, Liang and Guo, Shanshan and Han, Jianhua and Xu, Hang and Ma, Shikui and Liang, Xiaodan},
  journal={arXiv preprint arXiv:2306.10322},
  year={2023}
}
```
