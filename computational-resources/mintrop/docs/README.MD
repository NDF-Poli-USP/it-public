<p align="center">
  <img src="https://github.com/NDF-Poli-USP/it-public/blob/main/computational-resources/mintrop/docs/assets/ndf_logo_caption_colour-1%20(1).png" width="260"/>
</p>

<h1 align="center">🖥️ Mintrop HPC – Quick Start Guide</h1>

<p align="center">
  <b>Fluid Dynamics and Fluids Research Center (NDF) • Poli-USP</b>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/HPC-Cluster-blue"/>
  <img src="https://img.shields.io/badge/Scheduler-SLURM-green"/>
  <img src="https://img.shields.io/badge/Linux-Shell-lightgrey"/>
</p>

---

## 📌 Overview

**Mintrop** is a High-Performance Computing (HPC) cluster used for:

* Scientific simulations (CFD, FEM)
* Machine Learning / AI workloads
* Intensive data processing

---

## 🔑 Access

```bash
ssh user@MINTROP_IP
```

```bash
hostname
```

| Output    | Meaning      |
| --------- | ------------ |
| loginXX   | Headnode     |
| computeXX | Compute node |

---

## ⚠️ Most Important Rule

❌ Never run heavy workloads on the **headnode**
✔ Use it only for:

* Navigation
* File preparation
* Job submission

---

## 🚀 Execution

### 🔹 Interactive Mode (testing)

```bash
srun --pty bash -i
```

```bash
module load python
python script.py
```

🔙 Exit compute node:

```bash
exit
```

---

### 🔹 Batch Mode (production)

```bash
#!/bin/bash
#SBATCH --job-name=my_job
#SBATCH --cpus-per-task=8
#SBATCH --time=01:00:00

module purge
module load python

python script.py
```

```bash
sbatch job.sh
```

---

## 📊 Monitoring

```bash
squeue -u your_user
scancel JOB_ID
sinfo
```

---

## 📁 Directory Structure

### 🏠 `/home` (persistent storage)

* Shared across all nodes
* Permanent storage

✔ Use for:

* Scripts
* Final results
* Environments

⚠ Slower I/O (NFS)

---

### ⚡ `/scratch` (execution space)

* Local disk per node
* High performance
* Temporary (may be cleared after jobs)

✔ Use for:

* Job execution
* Intermediate data

---

## 🔁 Recommended Workflow (MANDATORY)

```bash
srun --pty bash -i

# copy data
cp -r ~/project /scratch/

# run
cd /scratch/project
python script.py

# save results
cp -r results ~/project/

# exit node
exit
```

---

## 🧠 Technical Concept

| Directory | Type  | Performance | Persistence |
| --------- | ----- | ----------- | ----------- |
| /home     | NFS   | Low         | High        |
| /scratch  | Local | High        | Low         |

---

## 📦 Modules

```bash
module purge
module avail
module load X
module list
```

---

## 🧵 Persistent Sessions

```bash
screen -S session
```

Detach:

```
Ctrl + A + D
```

Resume:

```bash
screen -x
```

---

## 🔄 Data Transfer

Send files:

```bash
rsync -av file user@host:~/destination/
```

Receive files:

```bash
rsync -av user@host:~/file ./local/
```

---

## ⚠️ Important Notes

* `/home` is shared across nodes
* `/scratch` is node-local
* DGX nodes have local `/home`
* Data loss is possible → keep backups

---

## 🔒 Best Practices

* Always test with `srun`
* Use `/scratch` for execution
* Never overload the headnode
* Use `module purge` before jobs
* Keep external backups

---

## 📚 Official Documentation

Refer to the full Mintrop documentation for:

* Advanced SLURM usage
* MPI / OpenMP
* Remote Jupyter
* OpenFOAM / Devito / Firedrake

---

## ✅ Conclusion

With this guide, you can:

* Access the cluster
* Run jobs correctly
* Use resources efficiently
* Follow HPC best practices

---

<p align="center">
  Developed for internal use at NDF • Poli-USP
</p>
