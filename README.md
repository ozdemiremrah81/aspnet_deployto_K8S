# aspnet_deployto_K8S
We are gonna deploy ASPnet web app to k8s
## Prereqs: 
Install Docker Desktop

Install minikube [https://minikube.sigs.k8s.io/docs/start/?arch=%2Fwindows%2Fx86-64%2Fstable%2F.exe+download](https://minikube.sigs.k8s.io/docs/start/)
### Steps
#### Step1
Download or clone all files in this repository to your environment. (i.e c:\asp-net-getting-started)
cd c:\asp-net-getting-started
& minikube -p minikube docker-env --shell powershell | Invoke-Expression

docker build -t aspnet .

kubectl apply -f .\aspnet.yaml

 echo "apiVersion: v1
   kind: Service
   metadata:
     name: my-service
   spec:
     type: NodePort
     selector:
       app: aspnet
     ports:
       - protocol: TCP
         port: 80
         targetPort: 80
         nodePort: 30000" >service.yaml

kubectl apply -f service.yaml

kubectl get services

 minikube service my-service
