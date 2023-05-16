# CI/CD with Crunchy Postgres for Kubernetes and Argo Part -1
# DRAFT

Continuous Integration / Continuous Delivery (CI/CD) is an automated approach in which incremental code changes are made made, built, tested and delivered.  GitOps plays an important part in enabling CI/CD.  If you are unfamiliar with Gitops and haven't seen [my blog](https://www.crunchydata.com/blog/postgres-gitops-with-argo-and-kubernetes) you may want to look at that before you proceed here.  In this blog we will build upon what learned in the GitOps blog.

Using Crunchy Postgres for Kubernetes, ArgoCD and Crunchy Postgres Self Test container, we will deploy a postgres cluster to a developer namespace, run a series of tests on the deployed cluster and then, once the tests pass, automatically deploy the same postgres cluster to a QA namespace.

## Requirements
 - The Crunchy Data Postgres Operator (PGO) v5.2 or later deployed in the kubernetes cluster.
 - ArgoCD v 2.6 or later deployed in the kubernetes cluster.
 - A git repository containing the Crunchy Postgres for Kubernetes manifest to be deployed.

## ArgoCD
