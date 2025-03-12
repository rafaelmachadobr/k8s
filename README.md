# Kubernetes - Implantando Nginx

Este repositório contém arquivos de configuração para implantar um aplicativo Nginx em um cluster Kubernetes.

## 🔧 Pré-requisitos

Antes de iniciar, certifique-se de ter os seguintes requisitos atendidos:

- [Kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/) instalado e configurado.
- Um cluster Kubernetes em funcionamento, como:
  - [Minikube](https://minikube.sigs.k8s.io/docs/start/) (De preferência)
  - [Kind](https://kind.sigs.k8s.io/docs/user/quick-start/)
  - [K3s](https://docs.k3s.io/quick-start)
  - [AKS (Azure Kubernetes Service)](https://docs.microsoft.com/pt-br/azure/aks/kubernetes-walkthrough-portal)

## 🛠 Passo a Passo

### 1. Clonar o Repositório

```bash
git clone https://github.com/rafaelmachadobr/k8s.git
```

### 2. Acessar a Pasta do Projeto

```bash
cd k8s
```

### 3. Criar um Cluster Kubernetes

Caso ainda não tenha um cluster Kubernetes rodando, você pode criar um usando Minikube ou Kind.

#### Usando Minikube:

```bash
minikube start
```

#### Usando Kind:

```bash
kind create cluster
```

Para verificar se o cluster foi criado corretamente, execute:

```bash
kubectl cluster-info
```

### 4. Aplicar os Arquivos de Configuração

Agora, aplique os manifests `deployment.yaml` e `service.yaml` para implantar o Nginx:

```bash
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
```

#### O que cada um faz?

- **Deployment** (`deployment.yaml`): Responsável por definir e gerenciar a implantação do Nginx. Ele garante que um número específico de réplicas do pod esteja sempre rodando e pode gerenciar atualizações do aplicativo sem tempo de inatividade.
- **Service** (`service.yaml`): Cria um serviço para expor os pods do deployment. Ele fornece um ponto de acesso estável para o Nginx, permitindo que outros componentes ou usuários acessem o aplicativo.

### 5. Verificar os Recursos Criados

Confirme se os pods e serviços foram criados corretamente:

```bash
kubectl get pods
kubectl get services
```

Se tudo estiver certo, o Nginx estará rodando no Kubernetes.

## 🔗 Acessando o Nginx

### Opção 1: Usando Port-Forward

Você pode acessar o Nginx localmente utilizando o `kubectl port-forward`:

```bash
kubectl port-forward svc/nginx-service 8080:80
```

Agora, abra o navegador e acesse:

```
http://localhost:8080
```

### Opção 2: Obtendo o IP Externo (Minikube)

Caso esteja usando Minikube, você pode expor o serviço com:

```bash
minikube service nginx-service
```

Isso abrirá o Nginx diretamente no navegador.

### Acessando o dashboard do Kubernetes

Você também pode acessar o dashboard do Kubernetes para visualizar os recursos implantados:

```bash
minikube dashboard
```

## 🧹 Limpeza

Para remover os recursos criados, execute:

```bash
kubectl delete -f deployment.yaml
kubectl delete -f service.yaml
```

Se você criou um cluster Kubernetes usando Minikube ou Kind, pode excluí-lo com:

```bash
minikube delete
kind delete cluster
```
