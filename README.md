# Experiment 6: Largest of Three Numbers, Git, Jenkins and Kubernetes

## 6(a) Python program and GitHub

Run the program:

```bash
python largest.py
```

Git commands (run in this folder):

```bash
git init
git add largest.py
git commit -m "Largest of three numbers program"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/Largest-of-Three-Numbers.git
git push -u origin main
```

Replace `YOUR_USERNAME` with your GitHub username.

## 6(b) Jenkins and Kubernetes sample application

Requirements: Docker Desktop, Minikube, kubectl, Jenkins and Git.

Run these commands from the `kubernetes-demo` folder in PowerShell:

```powershell
minikube start --driver=docker
docker build -t largest-app:1.0 .
minikube image load largest-app:1.0
kubectl apply -f deployment.yaml
kubectl rollout status deployment/largest-app
kubectl get pods
kubectl get services
minikube ip
```

Open `http://MINIKUBE_IP:30080` in a browser, replacing `MINIKUBE_IP` with the address returned by `minikube ip`.

### Jenkins Freestyle job

1. Open `http://localhost:8080`.
2. Create a Freestyle project named `Kubernetes-Deployment`.
3. Under Source Code Management, select Git and enter your repository URL; select branch `*/main`.
4. Add a Windows batch build step with:

```bat
docker build -t largest-app:1.0 .
minikube image load largest-app:1.0
kubectl apply -f deployment.yaml
kubectl rollout status deployment/largest-app
kubectl get pods
kubectl get services
```

5. Save, click Build Now, and inspect Console Output.

**Important:** Jenkins must run under a Windows account that can access Docker, Minikube and kubectl. Ensure these executables are on Jenkins' PATH and that the Minikube profile is available to the Jenkins service account.

Clean up the Kubernetes resources:

```bash
kubectl delete -f deployment.yaml
```
