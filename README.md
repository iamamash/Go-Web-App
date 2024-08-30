# Go Web Application

This is a simple website written in Golang. It uses the `net/http` package to serve HTTP requests.

## Running the Server Locally

To run the server locally, execute the following command:

```bash
go run main.go
```

The server will start on port 8080. You can access it by navigating to `http://localhost:8080/courses` in your web browser.

## Running the Server on AWS EKS

To deploy this application on an AWS EKS cluster, follow the steps below:

### 1. Create an EKS Cluster

First, create an EKS cluster using `eksctl`:

```bash
eksctl create cluster --name demo-cluster --region us-east-1
```

For more detailed instructions on setting up an EKS cluster, refer to `eks/install-eks-fargate.md`.

### 2. Deploy Application Resources

Apply the Kubernetes manifests to deploy the application on your EKS cluster:

```bash
kubectl apply -f k8s/.
```

### 3. Setup Ingress NGINX Controller

To handle incoming traffic, set up the NGINX Ingress Controller:

```bash
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.11.1/deploy/static/provider/aws/deploy.yaml
```

Refer to `ingress-controller/installation.md` for more details on setting up the Ingress NGINX Controller.

### 4. Setup ArgoCD

To manage continuous deployment, set up ArgoCD:

Follow the instructions in `gitops/argocd/install.md` to install ArgoCD on your cluster.

### 5. Access ArgoCD UI

Once ArgoCD is installed, access the ArgoCD UI and create a new project to manage your application's deployment.

### 6. Configure GitHub Actions for CI/CD

Set up GitHub Actions for continuous integration and deployment by configuring `.github/workflows/ci-cd.yaml` as per your project's requirements.

### 7. Deleting the EKS Cluster

After you are done, you can delete the EKS cluster to avoid unnecessary charges:

```bash
eksctl delete cluster --name demo-cluster --region us-east-1
```

## Looks like this

![Website](static/images/golang-website.png)

## Reference

For a detailed video guide on deploying Go applications on AWS EKS, check out this [video](https://youtu.be/HGu9sgoHaJ0?si=rAlvBobTZCoT-E1_).
