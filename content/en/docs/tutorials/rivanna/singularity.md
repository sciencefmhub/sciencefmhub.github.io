---
title: "Rivanna and Singularity"
linkTitle: "Singularity"
weight: 20
description: >-
     Singularity.
tags:
- rivanna
---


## Singularity

Singularity is a container runtime that implements a unique security model to 
mitigate privilege escalation risks and provides a platform to capture a complete 
application environment into a single file (SIF).

Singularity is often used in HPC centers.

University of Virginia granted us special permission to create
Singularity images on rivanna. We discuss here how to build and run
singularity images.

### Access

In order for you to be able to access singularity and build images, you must be in the
following groups:

```bash
biocomplexity
nssac_students
bii_dsc_community
```

To find out if you are, ssh into rivanna and issue the command

```bash
$ groups
```

If any of the groups is missing, please send Gregor an e-mail at
`laszewski@gmail.com`.

### Singularity cache

Before you can build images you need to set the singularity cache. This is due to the fact that the cache usually 
is created in your home directory and is often far too small for even our small projects. Thus you need to 
set it as follows

```bash
rivanna>
  mkdir -p /scratch/$USER/.singularity/cache
  export SINGULARITY_CACHEDIR=/scratch/$USER/.singularity/cache
```

Please remember that scratch is not permanent. In case you like a bit more permanent location you can alternatively use 

```bash
rivanna>
  mkdir -p /project/bii_dsc_community/$USER/.singularity/cache
  export SINGULARITY_CACHEDIR=/project/bii_dsc_community/$USER/.singularity/cache
```


### build.def

To build an image you will need a build definition file

We show next an exxample of a simple `buid.def` file that uses
internally a
[NVIDIA NGC PyTorch container](https://catalog.ngc.nvidia.com/orgs/nvidia/containers/pytorch).

```
Bootstrap: docker
From: nvcr.io/nvidia/pytorch:23.02-py3
```

Next you can follow the steps that are detailed in 
<https://docs.sylabs.io/guides/3.7/user-guide/definition_files.html#sections>

However, for Rivanna we MUST create the image as discussed next.

### Creating the Singularity Image

In order for you to create a singularity container from the
`build.def` file please login to either of the following special nodes
on Rivanna:

* `biihead1.bii.virginia.edu` 
* `biihead2.bii.virginia.edu`

For example: 

```bash
ssh $USER@biihead1.bii.virginia.edu
```

where $USER is your computing ID on Rivanna.

Now that you are logged in to the special node, you can create the
singularity image with the following command:

```bash
sudo /opt/singularity/3.7.1/bin/singularity build output_image.sif build.def
```

Note: **It is important that you type in only this command. If you modify
the name output_image.sif or build.def the command will not work and you will
recieve an authorization error.**

In case you need to rename the image to a better name please use the `mv` command.


In case you also need to have a different name other then build.def
the following Makefile is very useful. We assume you use `myimage.def`
and `myimage.sif`. Include it into a makefile such as:

```
BUILD=myimage.def
IMAGE=myimage.sif

image:
	cp ${BUILD} build.def
	sudo /opt/singularity/3.7.1/bin/singularity build output_image.sif build.def
	cp output_image.sif ${IMAGE}
	make -f clean

clean:
	rm -rf build.def output_image.sif
```

Having such a `Makefile` will allow you to use the command

```bash
make image
```

and the image `myimage.sif` will be created. with make clean you will
delete the temporary files `build.def` and `output_image.sif`
	
## Create a singularity image for tensorflow

TODO

## Work with Singularity container

Now that you have an image, you can use it while using the
documentation provided at 
<https://www.rc.virginia.edu/userinfo/rivanna/software/containers/>


### Run GPU images

To use NVIDIA GPU with Singularity, `--nv` flag is needed.

```basg
singularity exec --nv output_image.sif python myscript.py
```

TODO: THE NEXT PARAGRAPH IS WRONG

Since Python is defined as the default command to be excuted and
singularity passes the argument(s) after the image name,
i.e. myscript.py, to the Python interpreter. So the above singularity
command is equivalent to

```bash
singularity run --nv output_image.sif myscript.py
```

### Run Images Interactively

```bash
ijob  -A mygroup -p gpu --gres=gpu -c 1
module purge
module load singularity
singularity shell --nv output_image.sif
```

## Singularity Filesystem on Rivanna

The following paths are exposed to the container by default

* /tmp
* /proc
* /sys
* /dev
* /home
* /scratch
* /nv
* /project

### Adding Custom Bind Paths

For example, the following command adds the /scratch/$USER directory
as an overlay without overlaying any other user directories provided
by the host:

```bash
singularity run -c -B /scratch/$USER output_image.sif
```

To add the /home directory on the host as /rivanna/home inside the container:

```bash
singularity run -c -B /home:/rivanna/home output_image.sif
```

## FAQ

### Adding singularity to slurm scripts

TBD

### Running on v100

TBD

### Running on a100-40GB

TBD

### Running on a100-80GB

TBD

### RUnning on special fox node a100-80GB

TBD


