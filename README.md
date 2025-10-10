
# Online Boutique – GitOps com ArgoCD e Kubernetes

## Descrição
Projeto desenvolvido para praticar GitOps usando ArgoCD e Kubernetes, automatizando o deploy da aplicação Online Boutique composta por múltiplos microserviços.

## Pré-requisitos
- Kubernetes (Rancher Desktop ou similar) instalado e configurado
- Kubectl funcionando localmente
- Docker instalado
- Conta e repositório público no GitHub
- ArgoCD instalado no cluster Kubernetes
  ## Pré-requisitos
- Kubernetes (Rancher Desktop ou similar) instalado e configurado  
- Kubectl funcionando localmente  
- Docker instalado  
- Conta e repositório público no GitHub  
- ArgoCD instalado no cluster Kubernetes  
# Criar namespace do ArgoCD
kubectl create namespace argocd

# Instalar o ArgoCD no cluster
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

# Verificar os pods do ArgoCD
kubectl get pods -n argocd

# Fazer port-forward para acessar o painel do ArgoCD
kubectl port-forward svc/argocd-server -n argocd 8080:443

# Obter a senha inicial do admin
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d

# Obter a senha inicial do admin
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
mo executar
1. Faça o clone deste repositório.
2. Importe os manifests YAML no ArgoCD.
3. Sincronize a aplicação usando o ArgoCD.
4. Acesse o frontend via port-forward:
5. Depois, abra http://localhost:8081 no navegador.

## Evidências de funcionamento
- Todos os microserviços estão rodando no cluster

    ![kurbenetes](https://github.com/user-attachments/assets/c5b095c9-2992-4bf9-8bba-0e3705791a5f)
    ![kubernetes 2](https://github.com/user-attachments/assets/aa4bd8f8-29bd-48c6-ab90-68185fd738e1)

  
Etapas Extras: Integração com GitHub Privado e Helm Charts

⚙️ Passo a passo do que fazer agora
1️⃣ Verifique se você tem as chaves SSH

No terminal, rode:

ls ~/.ssh/


Você deve ver os arquivos:

id_rsa
id_rsa.pub


Se não existir, gere uma nova chave:

ssh-keygen -t rsa -b 4096 -C "seu_email@exemplo.com"



2️⃣ Copie o conteúdo da chave pública
cat ~/.ssh/id_rsa.pub




~/.ssh/id_rsa
~/.ssh/id_rsa.pub

🗝 Etapa 2: Adicionar a chave pública no GitHub

Copie o conteúdo da chave pública:

cat ~/.ssh/id_rsa.pub


Vá em https://github.com/settings/keys

Clique em New SSH Key

Cole o conteúdo copiado e salve.

⚙ Etapa 3: Adicionar a chave privada ao ArgoCD

No terminal, execute:

argocd repo add git@github.com:USUARIO/REPO_PRIVADO.git \
  --ssh-private-key-path ~/.ssh/id_rsa


Para confirmar a configuração:

argocd repo list


Se o repositório aparecer listado como Successful, a configuração está correta ✅

🧪 Etapa 4: Criar e sincronizar a aplicação no ArgoCD

Acesse o painel do ArgoCD

Clique em NEW APP

Configure:

Repository URL: git@github.com:USUARIO/REPO_PRIVADO.git


Destination: https://kubernetes.default.svc

Namespace: default

Clique em Create

Clique em SYNC para aplicar o deploy

🧱 2. Criar e estudar conceitos vinculados a Helm Charts
🎯 Objetivo

Compreender os conceitos de Helm Charts e aprender a empacotar, versionar e implantar uma aplicação usando o ArgoCD.

🧩 O que é um Helm Chart?

Um Helm Chart é um pacote de templates YAML que descreve uma aplicação Kubernetes, permitindo reutilização e parametrização através de variáveis definidas em values.yaml.

⚙ Etapa 1: Criar um Helm Chart

Crie um novo chart de exemplo:

helm create nginx-chart


Estrutura gerada:

nginx-chart/
├── Chart.yaml
├── values.yaml
└── templates/
     ├── deployment.yaml
     ├── service.yaml

🧾 Etapa 2: Configurar o values.yaml

Edite o arquivo values.yaml:

image:
  repository: nginx
  tag: latest
service:
  type: ClusterIP
  port: 80
replicaCount: 2

📦 Etapa 3: Empacotar o chart
helm package nginx-chart

🌐 Etapa 4: Adicionar ao repositório Git

Crie um diretório no seu repositório Git:

/helm/nginx-chart/


Envie o conteúdo do chart para o GitHub:

git add .
git commit -m "Adiciona Helm Chart do Nginx"
git push origin main

🚀 Etapa 5: Implantar com ArgoCD

No painel do ArgoCD, crie uma nova aplicação:

Application Name: nginx-helm

Repository URL: seu repositório Git

Path: /helm/nginx-chart

Project: default

Sync Policy: manual ou automática

Type: Helm

Clique em Create → Sync
O ArgoCD fará o deploy do chart automaticamente.

✅ Etapa 6: Testar a aplicação

Liste os pods:

kubectl get pods


Acesse a aplicação:

kubectl port-forward svc/nginx-helm 8080:80


Abra no navegador:
👉 http://localhost:8080

<img width="1486" height="759" alt="Captura de tela 2025-10-10 084143" src="https://github.com/user-attachments/assets/70527597-46c2-474b-a37d-c946c21c2f51" />

<img width="1478" height="761" alt="Captura de tela 2025-10-10 084340" src="https://github.com/user-attachments/assets/c1bc24f3-eb18-4e19-b9fd-be6b4cd8b111" />

  


  <img width="1920" height="954" alt="Captura de tela 2025-10-06 190124" src="https://github.com/user-attachments/assets/73eb05a1-ba42-4439-bbd7-d9372e718d29" />

<img width="1920" height="1080" alt="Captura de tela 2025-10-10 090634" src="https://github.com/user-attachments/assets/d0b21044-657d-4504-bf98-165972b86a09" />

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/76e05b9f-793b-429a-810b-f8a58931bcf4" />
