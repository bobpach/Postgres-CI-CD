# CI/CD with Crunchy Postgres for Kubernetes and Argo Part - 2
# DRAFT
This is the part 2 of CI/CD with Crunchy Postgres for Kubernetes and Argo.  We will pickup from where we left off in [part 1](https://github.com/bobpach/Postgres-CI-CD/tree/main/Part-1-Deployment). In this blog, we will use ArgoCD Image Updater to monitor a private Docker registry for changes to the image tag.  The image updater will update the image tags in github and the ArgoCD application will deploy those changes to the postgres-dev namespace.  Once deployed, the [self-test](https://github.com/bobpach/Crunchy-Postgres-Self-Test) will run and the changes will be applied to the postgres-qa namespace if all tests pass.

Let's begin.

## Argo CD Image Updater
[Argo CD Image Updater](https://argocd-image-updater.readthedocs.io/en/stable/) is a tool to automatically update the container images of Kubernetes workloads that are managed by Argo CD.  We will use it to monitor postgres container images in our private docker registry.

### Installation
We will install Argo CD Image updater into the argocd namespace in our kubernetes cluster.  We already have Argo CD installed there in the previous blog.

``` bash
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj-labs/argocd-image-updater/stable/manifests/install.yaml
```

You should now see it in your pod list:

```bash
kubectl -n argocd get po
NAME                                                READY   STATUS    RESTARTS      AGE
argocd-application-controller-0                     1/1     Running   0             4d16h
argocd-applicationset-controller-596ddc6c7d-b7qgw   1/1     Running   0             4d16h
argocd-dex-server-78c894df5b-r72v5                  1/1     Running   0             4d16h
argocd-image-updater-84ffbd4747-v2mkf               1/1     Running   0             4d16h
argocd-notifications-controller-6f65c4ccdb-8kns8    1/1     Running   0             4d16h
argocd-redis-7dd84c47d6-mdpkn                       1/1     Running   0             4d16h
argocd-repo-server-667d685cbc-nwrf4                 1/1     Running   0             4d16h
argocd-server-6cb4998447-slpkm                      1/1     Running   0             4d16h
```

