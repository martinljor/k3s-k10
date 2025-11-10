# k3s-k10
Build your own lab for k10 with k3s

sudo curl -sfL https://get.k3s.io | sh -

screen -d -m -L -Logfile /var/log/k3s.log k3s server

sudo curl https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3 | bash

cd 
sudo  mkdir .kube
sudo chown -R "martin" /home/martin/.kube/
sudo kubectl config view --raw >~/.kube/config

sudo helm repo add kasten https://charts.kasten.io/
sudo apt-get install jq -y
sudo curl https://docs.kasten.io/downloads/8.0.12/tools/k10_primer.sh | sudo bash

sudo kubectl create ns kasten-io

sudo helm install k10 kasten/k10 --namespace=kasten-io --kubeconfig /etc/rancher/k3s/k3s.yaml

sudo kubectl get pods -A
sudo kubectl get svc gateway -n kasten-io
sudo kubectl edit svc gateway -n kasten-io
*add externalIPs + Port 80 --> 8080 + ClusterIP --> NodePort
sudo kubectl get svc gateway -n kasten-io


