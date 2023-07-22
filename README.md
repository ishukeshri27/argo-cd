Argo-cd is a devops tool which helps in keeping the configuration of kubernetes cluster in sync with git taking git as the single source of truth and if any changes applied manully by devops team on kubertenes cluster it will role back the changes with git configuration 

##########################

steps to install argo cd on kuberentes cluster
1. Start minikube cluster using command minikube start --driver=your-hypervisor name (skipping these steps )
2. Create a namespace for argo-cd with command- kubectl create namespace argocd
3. run this command to install argo-cd- kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
4. check status of argo-cd using this-  kubectl get pod -n argocd && then get it service using command kubectl get svc -n argocd
5. port forward argo-cd server using this command - kubectl port-forward svc/argocd-server 8080:443 -n argocd
6. open local host and with port number on which it is listening
7. Login to UI using username as admin and passoword you will get using this command- kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 --decode && echo
8. Now run  kubectl apply -f application.yaml 
9. Make sure you put your repo link and path of your deployment and service in application.yaml
10. you can check all the things like manully making replicas to different value which is not there in deployment.yaml you will see it will automatically revert to git configuration rather than changes devops teams has done manully
