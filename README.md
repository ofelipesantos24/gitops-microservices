
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


  <img width="1920" height="954" alt="Captura de tela 2025-10-06 190124" src="https://github.com/user-attachments/assets/73eb05a1-ba42-4439-bbd7-d9372e718d29" />


<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/76e05b9f-793b-429a-810b-f8a58931bcf4" />
