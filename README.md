# Postgres-CI-CD
This is a two part series that covers deploying and updating [Crunchy Postgres from Kubernetes](https://www.crunchydata.com/products/crunchy-postgresql-for-kubernetes) (CPK) using ArgoCD.  Each section has an individual README.md that provides the steps to achieve the desired result.

## Part 1 - Deployment
This section focuses on deploying CPK into a dev namespace.  The deployment manifest includes a [Crunchy Postgres Self Test] container that tests the deployment to ensure that create, read, replication and delete functionality is working correctly in the postgres cluster.  If all tests pass, the self test container syncs an ArgoCD application to deploy the same manifest to a qa namespace.

## Part 2 - Update
//TODO:
