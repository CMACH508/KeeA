# KeeA*

This is the open-source codebase the paper: __KeeA*: Epistemic Exploratory A∗ Search via Knowledge Calibration__. The project page for this paper can be found on the <https://openreview.net/pdf?id=b8j0Gbg4N3>. Please do not hesitate to contact us if you have any problems.

## Description
In this paper, KeeA* search is proposed and the main contributions are summarized below.

- We theoretically demonstrate that cluster sampling produces a candidate set with more favorable extrema than uniform sampling by embedding distributional knowledge into the cluster structure, and increasing both the expected mean and variance of sampled nodes
contributes to improved decision-making performance.
- Cluster scouting and path-aware sampling are introduced by KeeA∗ to enhance the quality of the sampled candidate set by injecting epistemic knowledge into the sampling. We first show that for any two nodes, a greater disparity in their f-values corresponds to a higher likelihood that the node with the larger f also exhibits a greater true reward f*, despite the presence of prediction errors. Accordingly, cluster scouting is proposed by first evaluating clusters based on f-statistics and subsequently allocating a larger sampling budget to clusters with higher estimated quality to improve the expected mean of candidate nodes. Furthermore, path-aware sampling mechanism is proposed to incorporate historical path dependencies into the intra-cluster sampling process, thereby increase the variance of selected nodes.
- 
- Experiments are conducted on two real-world applications: retrosynthetic planning in organic chemistry and logic synthesis in VLSI design. KeeA∗ demonstrates superior performance over SeeA∗ and other state-of-the-art heuristic search algorithms, achieving higher success rates in problem-solving and superior solution quality.
## Retrosynthetic planning
### Preparation
The implemented of KeeA* on retrosynthetic planning task is built on the top of [Retro*](https://github.com/binghong-ml/retro_star) and [Retro*+](https://github.com/junsu-kim97/self_improved_retro)
You need to first install the Retro* lib by
```
pip install -e retro_star/packages/mlp_retrosyn
pip install -e retro_star/packages/rdchiral
pip install -e .
```
The building block molecules and cost estimator model are provided by [Retro*](https://www.dropbox.com/scl/fi/cchn0wjz8j0dqxhr0qrom/retro_data.zip?rlkey=kqz60ec7vx7087vg1o63nucyo&e=1&dl=0). The employed single-step policy model is provided by the [Retro*+](https://drive.google.com/drive/u/0/folders/13DdftEV0x55OZ8ZxHNAkmcvi_4x90hPI). Test dataset is provided in the attached file.

### Dependencies
```
rdkit==2022.9.3
torch==1.13.1
pandas==1.3.5
numpy==1.21.5
```

### Implementation
Run the SeeA algorithm under uniform sampling strategy, clustering sampling strategy, and UCT-like sampling strategy based on the following code.
```
python Cluster_sampling.py
```

## Logic synthesis

### Preparation
Yosys package is needed to process the AIG graph from <https://github.com/YosysHQ/yosys>, which is a framework for RTL synthesis tools. The test chips are provided in the attachment. The lib file need to be downloaded from <https://drive.google.com/file/d/1asSHhyswfGoAbt2g2BEx7ZpHL_QjWE3T/view?usp=sharing>.

### Implementation
If you want to test a circuit, please run
```
python Clustering_sampling.py --chips 'alu4' --gpu 0 --thread 0
```
