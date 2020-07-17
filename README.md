Instalando ELK-STACK no AKS

ELK Cluster Kubernetes
Cluster Name: akspriv-elk-poc
RG: rg-elk-app-poc

az aks get-credentials --name akspriv-elk-poc --resource-group rg-elk-app-poc --admin

Namespace
elastic-stack
elastic-system

Processo de Instalação

kubectl apply -f https://download.elastic.co/downloads/eck/0.9.0/all-in-one.yaml

>elastic
kubectl apply -f elk-conf.yaml -n elastic-stack

>apm
kubectl apply -f apm-conf.yaml -n elastic-stack

>kibana
kubectl apply -f kb-config.yaml -n elastic-stack

echo `kubectl get secret elk-cluster-es-elastic-user -o=jsonpath='{.data.elastic}' -n elastic-stack| base64 --decode`

user: elastic
secret: j7m4cwnhcmjgq78d7dsbv4vj

---Comandos para validar o status dos deployments
kubectl get elasticsearch,kibana,apmserver -n elastic-stack
kubectl get services -n elastic-stack
kubectl get services -n elastic-stack


kubectl port-forward service/kibana-kb-http 5601 -n elastic-stack
