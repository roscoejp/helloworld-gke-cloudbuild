# helloworld-gke-cloudbuild

Primary purpose of this repo is to provide a quick build to demo Cloud Build deployments to Private Endpoint enabled GKE clusters.

## Requirements

- A Zonal GKE cluster (regional not supported for this but should be an easy patch if needed).
- A GKE API Proxy deployment and exposing service
- A Google Cloud Build trigger

### Notes

- Since pods communicate with their master via the private endpoint by default, the GKE API Proxy deployment will act as a reverse-proxy to the GKE master. The exposing service should be publicly accessible.
- The Google Cloud Build trigger should set the following substitutions:

| Variable | Description | Default Value | Required |
| --- | --- | --- | --- |
| `_GKE_CLUSTER` | Name of the GKE cluster that will be getting accessed. This value is only used to obtain the credentials of the cluster. | `my-cluster` | :heavy_check_mark: |
| `_K8S_API_PROXY` | URL or IP address of the GKE API proxy exposing service. | `127.0.0.1` | :heavy_check_mark: |
| `_K8S_API_PROXY_PORT` | Port on which the GKE API proxy is exposed. | `8118` | :heavy_multiplication_x: |
| `_ZONE` | Zone of the GKE cluster that will be getting accessed. This value is only used to obtain the credentials of the cluster. | `us-east1-c` | :heavy_check_mark: |
| `_WORKERPOOL_PROJECT_ID` | Project ID where the custom worker pool is registered. | `my-project` | :heavy_check_mark: |
| `_WORKERPOOL_REGION` | Region in which the custom worker pool is registered. | `us-east1` | :heavy_check_mark: |
| `_WORKERPOOL_NAME` | Name of the custom worker pool. | `workerpool` | :heavy_check_mark: |
