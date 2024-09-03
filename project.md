do prerequisite first

go to eks console

in cmd

create eks cluster
```
eksctl create cluster --name demo-cluster --region <name> --fargate
```

go to the console and see cluster is created or not

update kubeconfig file
```
aws eks update-kubeconfig --name demo-cluster --region <rname>
```
### Deploy of application

# 2048 App

## Create Fargate profile

```
eksctl create fargateprofile \
    --cluster demo-cluster \
    --region us-east-1 \
    --name alb-sample-app \
    --namespace game-2048
```

## Deploy the deployment, service and Ingress

```
kubectl apply -f https://raw.githubusercontent.com/kubernetes-sigs/aws-load-balancer-controller/v2.5.4/docs/examples/2048/2048_full.yaml
```



![Screenshot 2023-08-03 at 7 57 15 PM](https://github.com/iam-veeramalla/aws-devops-zero-to-hero/assets/43399466/93b06a9f-67f9-404f-b0ad-18e3095b7353)

check the pod
kubectl get pods -n game-2048

watch the pod 
kubectl get pods -n game-2048 -w

service
kubectl get svc -n game-2048

ingress 
kubectl get ingress -n game-2048
if you notice there is no address because no lb or ingress controller

# commands to configure IAM OIDC provider 

```
export cluster_name=demo-cluster
```

```
oidc_id=$(aws eks describe-cluster --name $cluster_name --query "cluster.identity.oidc.issuer" --output text | cut -d '/' -f 5) 
```

## Check if there is an IAM OIDC provider configured already

- aws iam list-open-id-connect-providers | grep $oidc_id | cut -d "/" -f4\n 

If not, run the below command

```
eksctl utils associate-iam-oidc-provider --cluster $cluster_name --approve
```

