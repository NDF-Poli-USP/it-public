<p align="center">
  <img src="./docs/assets/logo-ndf.png" width="260"/>
</p>

<h1 align="center">🖥️ Mintrop HPC – Quick Start Guide</h1>

<p align="center">
  <b>Núcleo de Dinâmica e Fluidos (NDF) • Poli-USP</b>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/HPC-Cluster-blue"/>
  <img src="https://img.shields.io/badge/Scheduler-SLURM-green"/>
  <img src="https://img.shields.io/badge/Linux-Shell-lightgrey"/>
</p>

---

## 📌 Overview

O **Mintrop** é um cluster HPC utilizado para:

* Simulações científicas (CFD, FEM)
* Machine Learning / AI
* Processamento intensivo

---

## 🔑 Acesso

```bash
ssh usuario@IP_DO_MINTROP
```

```bash
hostname
```

| Resultado | Significado  |
| --------- | ------------ |
| loginXX   | Headnode     |
| computeXX | Compute node |

---

## ⚠️ Regra mais importante

❌ Nunca rode código pesado no **headnode**
✔ Use apenas para:

* Navegação
* Preparação
* Submissão

---

## 🚀 Execução

### 🔹 Interativo (teste)

```bash
srun --pty bash -i
```

```bash
module load python
python script.py
```

🔙 Sair do nó:

```bash
exit
```

---

### 🔹 Batch (produção)

```bash
#!/bin/bash
#SBATCH --job-name=meu_job
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

## 📊 Monitoramento

```bash
squeue -u seu_usuario
scancel JOB_ID
sinfo
```

---

## 📁 Estrutura de diretórios

### 🏠 `/home` (persistente)

* Compartilhado entre todos os nós
* Armazenamento permanente

✔ Use para:

* Scripts
* Resultados finais
* Ambientes

⚠ Mais lento (NFS)

---

### ⚡ `/scratch` (execução)

* Disco local do nó
* Alta performance
* Temporário (pode ser limpo)

✔ Use para:

* Execução de jobs
* Dados intermediários

---

## 🔁 Fluxo correto (OBRIGATÓRIO)

```bash
srun --pty bash -i

# copiar dados
cp -r ~/projeto /scratch/

# executar
cd /scratch/projeto
python script.py

# salvar resultados
cp -r resultados ~/projeto/

# sair do node
exit
```

---

## 🧠 Conceito técnico

| Diretório | Tipo  | Performance | Persistência |
| --------- | ----- | ----------- | ------------ |
| /home     | NFS   | Baixa       | Alta         |
| /scratch  | Local | Alta        | Baixa        |

---

## 📦 Módulos

```bash
module purge
module avail
module load X
module list
```

---

## 🧵 Sessões persistentes

```bash
screen -S sessao
```

Desanexar:

```
Ctrl + A + D
```

Retornar:

```bash
screen -x
```

---

## 🔄 Transferência de dados

Enviar arquivos:

```bash
rsync -av arquivo user@host:~/destino/
```

Receber arquivos:

```bash
rsync -av user@host:~/arquivo ./local/
```

---

## ⚠️ Observações importantes

* `/home` é compartilhado entre nós
* `/scratch` é local por nó
* DGX possui `/home` local
* Dados podem ser perdidos → faça backup

---

## 🔒 Boas práticas

* Sempre testar com `srun`
* Usar `/scratch` para execução
* Nunca sobrecarregar o headnode
* Usar `module purge` antes de rodar jobs
* Fazer backup externo

---

## 📚 Documentação oficial

Consulte os tutoriais completos do Mintrop para:

* SLURM avançado
* MPI / OpenMP
* Jupyter remoto
* OpenFOAM / Devito / Firedrake

📎 Referência interna:


---

## ✅ Conclusão

Com este guia você consegue:

* Acessar o cluster
* Executar jobs corretamente
* Utilizar recursos de forma eficiente
* Seguir boas práticas de HPC

---

<p align="center">
  Desenvolvido para uso interno do NDF • Poli-USP
</p>
