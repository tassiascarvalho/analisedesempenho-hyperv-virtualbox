# analisedesempenho-hyperv-virtualbox
Repositório com os testes de desempenho realizados no âmbito do artigo “Análise de Desempenho Atualizada de um Hypervisor Nativo vs Host-Based Hypervisor”, comparando o Microsoft Hyper-V e o Oracle VirtualBox em cenários de CPU, memória e disco. Os testes foram realizados com PerformanceTest e Fio sob condições controladas.

# Comparação de Desempenho: Hyper-V vs VirtualBox

Este repositório contém os testes de desempenho realizados para comparar dois hypervisors amplamente utilizados:

- **Microsoft Hyper-V** (hypervisor nativo)
- **Oracle VirtualBox 7.1.6** (hypervisor host-based)

## 🎯 Objetivo

Avaliar o desempenho de cada hypervisor em três dimensões principais:

- CPU
- Memória
- Disco (I/O)

Todos os testes foram realizados com a mesma configuração de máquina virtual (Ubuntu 24.10 LTS, 8 CPUs, 8 GB RAM, 40 GB SSD).

---

## 🛠️ Configuração Experimental

| Componente            | Especificação                      |
|-----------------------|------------------------------------|
| Processador           | Intel Core i7-11800H @ 2.30GHz     |
| RAM                   | 16 GB DDR4                         |
| Sistema Host          | Windows 11 Education 64 bits       |
| Hypervisor Nativo     | Microsoft Hyper-V                  |
| Hypervisor Host-Based | Oracle VirtualBox 7.1.6            |
| Sistema Convidado     | Ubuntu 24.10 LTS (64 bits)         |
| Benchmarks            | PerformanceTest e Fio              |

---

## ⚙️ Comandos Executados

### 📌 CPU e Memória – com PerformanceTest

```bash
./pt_linux_x64 -r 3 -D 2 -i 3 > cpu_medium.txt
./pt_linux_x64 -r 3 -D 4 -i 3 > cpu_muitolongo.txt

Parâmetros:
-r 3: executa os testes combinados de CPU e memória.
-D 2: duração média.
-D 4: duração muito longa.
-i 3: repete o teste três vezes.

### 📌 Disco (I/O) – com Fio

Leitura sequencial:
```bash
fio --name=seq_read --ioengine=libaio --iodepth=16 --rw=read --bs=1M --direct=1 --size=4G --numjobs=3 --runtime=60 --group_reporting > seq_read_results.txt

Leitura e escrita combinadas:
```bash
fio --name=rw_seq --ioengine=libaio --iodepth=16 --rw=readwrite --rwmixread=50 --bs=1M --direct=1 --size=4G --numjobs=3 --runtime=60 --group_reporting > rw_seq_results.txt

📖 Referência
Artigo científico: Análise de Desempenho Atualizada de um Hypervisor Nativo vs Host-Based Hypervisor

Autores: Israel Torres, Tássia de Carvalho
Universidade da Beira Interior, 2025
