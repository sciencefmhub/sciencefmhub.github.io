---
title: "Rivanna Pod"
linkTitle: "Rivanna Pod"
weight: 15
description: >
  Rivanna
tags:
- rivanna
---



This documentation is so far only useful for betatesters. In this
group we have

* Gregor von Laszewski



The rivanna documentation for the basic pod is available at 

<https://www.rc.virginia.edu/userinfo/rivanna/basepod/>

 

## Introducing the NVIDIA DGX BasePOD

Rivanna contains a BasePod with 

* 10 DGX A100 nodes 
* 8 A100 GPU devices 
* 2 TB local node memory (per node) 
* 80 GB GPU memory (per GPU device)
 
The following Advanced Features have now been enabled  on the BasePOD:

* NVLink for fast multi-GPU communication
* GPUDirect RDMA Peer Memory for fast multi-node multi-GPU communication
* GPUDirect Storage with 200 TB IBM ESS3200 (NVMe) SpectrumScale storage array
 
What this means to you is that the POD is ideal for the following scenarios:

* The job needs multiple GPUs and/or even multiple nodes.
* The job (can be single- or multi-GPU) is I/O intensive.
* The job (can be single- or multi-GPU) requires more than 40 GB GPU
  memory. (We have 12 A100 nodes in total, 10 of which are the POD and
  2 are regular with 40 GB GPU memory per device.)
 
Detailed specs can be found in the official document (Chapter 3.1):
 
* <https://docs.nvidia.com/dgx-basepod-reference-architecture-dgx-a100-and-dgx-h100.pdf>
 
 
## Accessing the POD
 
### Allocation

A single job can request up to 4 nodes with 32
GPUs. Before running multi-node jobs, please make sure it can scale
well to 8 GPUs on a single node.
 
 
 
Slurm script
Please include the following lines:

```
#SBATCH -p gpu
#SBATCH --gres=gpu:a100:X # replace X with the number of GPUs per node
#SBATCH -C gpupod
 ```

### Open OnDemand

In *Optional: Slurm Option* write:

```
-C gpupod
```

### Interactive login

Interactive login to the nodes should be **VERY** limited and you need to use 
for most activities the batch queue. In case you need to look at thisng you can 
use our cloudmesh progarm to do so

Make sure to have vpn enabled and cloumdesh-rivanna installed via pip.
| computer> |
| --- |

  cms rivanna login a100-pod
```
 
Will log you into a node. The time is set by default to 30 minutes. 
Please immediatly log out after you are done with your work interactive 
work.

## Usage examples
 
### Deep learning

We will be migrating toward NVIDIA’s NGC containers for deep learning
frameworks such as PyTorch and TensorFlow, as they have been heavily
optimized to achieve excellent multi-GPU performance. These containers
have not yet been installed as modules but can be accessed under
/share/resources/containers/singularity:

* pytorch_23.03-py3.sif
* tensorflow_23.03-tf1-py3.sif
* tensorflow_23.03-tf2-py3.sif

(NGC has their own versioning scheme. The PyTorch and TensorFlow
versions are 2.0.0, 1.15.5, 2.11.0, respectively.)
 
The singularity command is of the form:

```
singularity run --nv /path/to/sif python /path/to/python/script
```

**Warning:** Distributed training is not automatic! Your code must be
parallelizable. If you are not familiar with this concept, please
visit:

* TF distributed training <https://www.tensorflow.org/guide/distributed_training>
* PyTorch DDP <https://pytorch.org/docs/stable/notes/ddp.html>
 
### MPI codes

Please check the manual for your code regarding the relationship
between the number of MPI ranks and the number of GPUs. For
computational chemistry codes (e.g. VASP, QuantumEspresso, LAMMPS) the
two are oftentimes equal, e.g.

```
#SBATCH --gres=gpu:a100:8
#SBATCH --ntasks-per-node=8
```

If you are building your own code, please load the modules nvhpc and
cuda which provide NVIDIA compilers and CUDA libraries. The compute
capability of the POD A100 is 8.0.
 
For documentation and demos, refer to the *Resources* section at the
bottom of this page: <https://developer.nvidia.com/hpc-sdk>
 
 
We will be updating our website documentation gradually in the near
future as we iron out some operational specifics. GPU-enabled modules
are now marked with a (g) in the *module avail* command as shown
below:


TODO: output from maodule avail to be included
 
 
