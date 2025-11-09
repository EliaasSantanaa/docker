# Orquestração de Containers com Kubernetes: Desafio Web Solutions Ltda.

Este projeto é a Prova de Conceito (PoC) desenvolvida para o desafio da empresa "Web Solutions Ltda.", como parte do trabalho acadêmico sobre Containers e Kubernetes.

O objetivo é modernizar a infraestrutura da empresa, migrando de um modelo tradicional de máquinas virtuais para uma arquitetura baseada em containers orquestrados. Esta solução demonstra a capacidade de rodar dois servidores web distintos (Nginx e Apache) de forma independente e escalável em um único cluster Kubernetes.

## 🎯 Desafio Resolvido

- **Nginx** é implantado e exposto na porta `8080`.
- **Apache HTTPD** é implantado e exposto na porta `8081`.
- Ambos os servidores utilizam imagens Docker customizadas, criadas a partir de `Dockerfiles` otimizados (usando a base `alpine`).
- A implantação é gerenciada por objetos `Deployment` do Kubernetes.
- O acesso externo é habilitado por objetos `Service` do Kubernetes, utilizando o tipo `LoadBalancer` para integração com o Docker Desktop.

## 🛠️ Pré-requisitos

Para executar este projeto, você precisará de:

1.  **Docker Desktop** (para Windows ou macOS).
2.  **Kubernetes** habilitado dentro do Docker Desktop:
    - Vá em `Settings` > `Kubernetes` > Marque a caixa `Enable Kubernetes`.
3.  Um terminal (PowerShell, CMD ou Git Bash/MINGW64).

## 📂 Estrutura do Projeto

```
workspace_docker/
├── README.md
├── apache/
│   ├── Dockerfile
│   └── index.html
├── nginx/
│   ├── Dockerfile
│   └── index.html
├── apache-config.yaml
└── nginx-config.yaml
```

## 🚀 Como Executar a Solução

Siga os passos abaixo no seu terminal, a partir da pasta raiz do projeto.

### Passo 1: Construir as Imagens Docker

Primeiro, construímos as imagens Docker customizadas que serão usadas pelo Kubernetes.

```powershell
# 1. Construir a imagem do Nginx
docker build -t meu-nginx:v1 ./nginx

# 2. Construir a imagem do Apache
docker build -t meu-apache:v1 ./apache
```

### Passo 2: Aplicar as Configurações no Kubernetes

Agora implantamos os serviços no cluster Kubernetes.

```powershell
# 1. Aplicar a configuração do Nginx (cria o Deployment e o Service)
kubectl apply -f nginx-config.yaml

# 2. Aplicar a configuração do Apache (cria o Deployment e o Service)
kubectl apply -f apache-config.yaml
```

**Ou, se estiver usando a pasta k8s:**

```powershell
# Aplicar todas as configurações da pasta k8s
kubectl apply -f k8s/
```

### Passo 3: Verificar os Serviços

```powershell
# Listar os pods criados
kubectl get pods

# Listar os serviços e verificar as portas expostas
kubectl get services
```

### Passo 4: Acessar os Servidores Web

Abra seu navegador e acesse:

- **Nginx**: http://localhost:8080
- **Apache**: http://localhost:8081

## 🧪 Comandos Úteis

```powershell
# Ver logs de um pod específico
kubectl logs <nome-do-pod>

# Ver detalhes de um deployment
kubectl describe deployment nginx-deployment

# Escalar um deployment
kubectl scale deployment nginx-deployment --replicas=3

# Deletar todos os recursos
kubectl delete -f nginx-config.yaml
kubectl delete -f apache-config.yaml
```

## 📝 Conclusão

Esta PoC demonstra com sucesso a migração para uma arquitetura moderna baseada em containers e Kubernetes, proporcionando:

- ✅ Isolamento entre serviços
- ✅ Facilidade de escalabilidade
- ✅ Gerenciamento simplificado
- ✅ Portabilidade entre ambientes

---

**Desenvolvido por:** [Elias Santana Santos - 97351]  
**Disciplina:** Containers e Kubernetes  
**Ano:** 2025