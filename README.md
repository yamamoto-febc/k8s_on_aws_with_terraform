# How To Deploy Kubernetes Clusters on AWS using Terraform and Terraform RKE Provider

This repository is an examples for building a Kubernetes cluster using Terraform and Terraform RKE provider on AWS.

> ref: [https://rancher.com/blog/2018/2018-05-14-rke-on-aws/](https://rancher.com/blog/2018/2018-05-14-rke-on-aws/)

## How to use

### Requirements

- [terraform](https://terraform.io) v0.11+
- [terraform-provider-rke](https://github.com/yamamoto-febc/terraform-provider-rke)
- Valid AWS access_key and secret_key
- [optional] `kubectl` command

### Deploy Kubernetes Cluster on AWS

```console
#clone this repo
$ git clone https://github.com/yamamoto-febc/k8s_on_aws_with_terraform.git
$ cd k8s_on_aws_with_terraform

#set API keys to environment variables
$ export AWS_ACCESS_KEY_ID="<your-access-key>"
$ export AWS_SECRET_ACCESS_KEY="<your-secret-key>" 

#deploy
$ terraform init && terraform apply

###########################################################################
#When "terraform apply" is completed, 
#kubeconfig file should be created in the current directory 
###########################################################################

#set KUBECONFIG environment variable for kubectl 
$ export KUBECONFIG=${PWD}/kube_config_cluster.yml 

###########################################################################
#Then, kubectl command can be used
###########################################################################

#component statuses
$ kubectl get cs

NAME                 STATUS    MESSAGE              ERROR
controller-manager   Healthy   ok                   
scheduler            Healthy   ok                   
etcd-0               Healthy   {"health": "true"}  

#nodes
$ kubectl get nodes

NAME                                             STATUS    ROLES               AGE       VERSION
ip-xx-xx-xx-xx.ap-northeast-1.compute.internal   Ready     controlplane,etcd   1m        v1.10.1
ip-xx-xx-xx-xx.ap-northeast-1.compute.internal   Ready     worker              1m        v1.10.1
ip-xx-xx-xx-xx.ap-northeast-1.compute.internal   Ready     worker              1m        v1.10.1
ip-xx-xx-xx-xx.ap-northeast-1.compute.internal   Ready     worker              1m        v1.10.1
```

## License

  This project is published under [Apache 2.0 License](LICENSE.txt).
  
## Author

  * Kazumichi Yamamoto ([@yamamoto-febc](https://github.com/yamamoto-febc))