### 🐳 SYS.SWARM // VAGRANT CLUSTER PROTOCOL

> **"Infraestrutura não é só subir container — é orquestrar caos com previsibilidade."**

<div align="center">
  <img src="https://img.shields.io/badge/Vagrant-1868F2?style=for-the-badge&logo=vagrant&logoColor=white" alt="Vagrant" />
  <img src="https://img.shields.io/badge/VirtualBox-183A61?style=for-the-badge&logo=virtualbox&logoColor=white" alt="VirtualBox" />
  <img src="https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white" alt="Docker" />
  <img src="https://img.shields.io/badge/Docker_Swarm-0db7ed?style=for-the-badge&logo=docker&logoColor=white" alt="Docker Swarm" />
  <img src="https://img.shields.io/badge/Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black" alt="Linux" />
  <img src="https://img.shields.io/badge/DevOps-000000?style=for-the-badge&logo=github&logoColor=white" alt="DevOps" />
</div>
<br>

Este repositório demonstra a criação de um **cluster distribuído com Docker Swarm**, provisionado automaticamente utilizando **Vagrant + VirtualBox**.

A proposta aqui não é apenas rodar containers — mas sim simular um ambiente de **infraestrutura real**, com múltiplos nós, comunicação em rede privada e orquestração automatizada.

---

## ⚙️ Arquitetura do Cluster

- 🧠 **Manager Node (Master)**
  - Responsável por orquestrar o cluster
  - Inicializa o Swarm
  - Distribui tarefas para os workers

- ⚙️ **Worker Nodes (node01, node02, node03)**
  - Executam containers
  - Se conectam automaticamente ao cluster via token

- 🌐 **Rede Privada**
  - Comunicação via IP fixo (`192.168.56.x`)
  - Isolamento total do ambiente

- 📦 **Provisionamento Automatizado**
  - Instalação do Docker via script
  - Inicialização do cluster
  - Join automático dos nodes

---

## 🧬 Topologia



```
        ┌──────────────┐
        │   MASTER     │
        │ 192.168.56.10 │
        │   (Manager)  │
        └──────┬───────┘
               │
    ┌──────────┼──────────┐
    │          │          │
┌────────┐ ┌────────┐ ┌────────┐
│ node01 │ │ node02 │ │ node03 │
│ .11    │ │ .12    │ │ .13    │
│Worker  │ │Worker  │ │Worker  │
└────────┘ └────────┘ └────────┘

````

---

## 🚀 Quick Start (Subindo o Cluster)

### 1. Clone o repositório

```bash
git clone https://github.com/Poliih/docker-swarm-vagrant.git
cd docker-swarm-vagrant
````

---

### 2. Suba o ambiente completo

```bash
vagrant up
```

👉 Isso vai:

* Criar 4 VMs
* Instalar Docker em todas
* Inicializar o Swarm
* Conectar automaticamente os nodes

---

### 3. Acesse o master

```bash
vagrant ssh master
```

---

### 4. Verifique o cluster

```bash
docker node ls
```

✔ Esperado:

```
master   Ready   Leader
node01   Ready
node02   Ready
node03   Ready
```

---

## 🌐 Deploy de Serviço (Teste real)

```bash
docker service create --name web --replicas 3 -p 8080:80 nginx
```

👉 Isso cria um serviço distribuído entre os nodes.

---

### 🔎 Ver distribuição

```bash
docker service ps web
```

---

### 🌍 Acessar no navegador

```
http://localhost:8080
```

---

## 🔥 Teste de Resiliência (Auto-Healing)

Simule falha de infraestrutura:

```bash
vagrant halt node01
```

Depois:

```bash
docker service ps web
```

👉 O Swarm recria automaticamente os containers em outros nodes.

💡 Isso é **alta disponibilidade na prática**.

---

## ⚡ Comandos Úteis

**Escalar serviço:**

```bash
docker service scale web=6
```

**Atualização sem downtime:**

```bash
docker service update --image nginx:alpine web
```

**Listar serviços:**

```bash
docker service ls
```

**Remover serviço:**

```bash
docker service rm web
```

---

## 🧠 Conceitos Demonstrados

* Orquestração de containers
* Cluster distribuído
* Alta disponibilidade
* Auto-healing
* Deploy escalável
* Infraestrutura como código (IaC)


---

## 🧠 Filosofia

> **"Se você consegue quebrar sua infra e ela se reconstrói sozinha — você fez certo."**

---

## 🚀 Próximos passos

* Load Balancer (Traefik / Nginx)
* Deploy de APIs reais
* Integração com CI/CD
* Migração para Kubernetes

---

## 🧑‍💻 Autor

Projeto focado em aprendizado prático de **DevOps, containers e orquestração distribuída**.

