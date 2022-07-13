# Argo Cd deployment (separate from automation)
    - 1st OpenShift (Argo CD and Kong CP)
    - 2nd OpenShift (Kong Data Plane + kuma remote control plane = App)
    - operator deployment
    - Getting the password of UI
    - import the CP and DP clusters

# OpenShift Deployment
## Kong Gateway Control Plane - Iteration 1 (94% of business)
    - Pre-requisites
        - create ns for kong
        - Create RBAC rules
    - Infra components
        - create license secret (first manually)
            - Then using hashicorp vault (In 2nd iteration) 
                - https://cloud.redhat.com/blog/how-to-use-hashicorp-vault-and-argo-cd-for-gitops-on-openshift [The blog is incorrect]
        - Generate cert + secret 
        - Postgresql
    -  Deploy control plane 
        - Variation from what we have done? - For postgres, we need to use the postgres subchart from kong
        - Best practice - use helm values (cp-values.yaml) (+) use kustomize
    - Post-Install of Kong control plane 
        - Exposing the service
        - Exposing the route
        - Update the ADMIN_URI in the deployment
        - Export cluster/cluster telemetry endpoints
    - Validaion 
        - Management UI
        - admin endpoint
        - Any other additional validation
    - Technical notes
        - Order-Dependent Deployments 
            - https://argo-cd.readthedocs.io/en/stable/user-guide/sync-waves/
    - References
        - https://argo-cd.readthedocs.io/en/stable/

## Kong Gateway Data Plane - Iteration 1 (94% of business)
    - Pre-requisites
        - same as above
    - Infra component
        - same as above
        - (-) postgresql?
        - (+) Keycloak server
        - (+) Monitoring infra (Prometheus + grafana)
    - Deploy data plane (using dp-values.yaml)
    - Patch the deployment for CLUSTER_URL & CLUSTER_TELEMETRY_URL
    - Post install of kong dp
    - validation
        - check clustering
        - any additional validation
    - Technical Notes
        - Order - dependent deployments (https://argo-cd.readthedocs.io/en/stable/user-guide/sync-waves/)
        - References
        - https://argo-cd.readthedocs.io/en/stable/


## Kong Mesh Control Plane - Iteration2
## Kong Mesh Data Plane - Iteration2


# Hybrid deployment - 1

## Kong Gateway Control Plane (VM)
## Kong Gateway Data Plane (OCP)
## Kong Mesh Global Control Plane (VM)
## Kong Mesh Remote Control Plane (OCP)


# Hybrid deployment - 2

## Kong Gateway Control Plane (OCP)
## Kong Gateway Data Plane (VM)
## Kong Mesh Global Control Plane (OCP)
## Kong Mesh Remote Control Plane (VM)

# Both CP and DP on VMs (outside Red Hat Scope)