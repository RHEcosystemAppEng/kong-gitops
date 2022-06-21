# Argo Cd deployment (separate from automation)
    - 1st OpenShift (Argo CD and Kong CP)
    - 2nd OpenShift (Kong Data Plane + kuma remote control plane = App)
    - operator deployment
    - Getting the password of UI
    - import the CP and DP clusters

# OpenShift Deployment
    ## Kong Gateway Control Plane 
        - Pre-requisites
            - create ns for kong
            - Create RBAC rules
        - Infra components
            - create license secret (first manually)
                - Then using hashicorp vault (In 2nd iteration) 
                    - https://cloud.redhat.com/blog/how-to-use-hashicorp-vault-and-argo-cd-for-gitops-on-openshift
            - Generate cert + secret 
            - Monitoring infra (Prometheus + grafana)
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

    ## Kong Gateway Data Plane
        - Pre-requisites
            - same as above
        - Infra component
            - same as above
            - (+) Keycloak server
        - Deploy data plane (using dp-values.yaml) - use kustomize
        - Post install of kong dp
        - validation
            - check clustering
            - any additional validation
        - Technical Notes
            - Order - dependent deployments (https://argo-cd.readthedocs.io/en/stable/user-guide/sync-waves/)
            - References
            - https://argo-cd.readthedocs.io/en/stable/

        
    ## Kong Mesh Control Plane
    ## Kong Mesh Data Plane


# Hybrid deployment (CP - on AWS VM and DP - on OpenShift clusters)

## Kong Gateway Control Plane 
## Kong Gateway Data Plane
## Kong Mesh Control Plane
## Kong Mesh Data Plane


# Hybrid deployment (CP - on OpenShift clusters and DP - on AWS VM)

## Kong Gateway Control Plane 
## Kong Gateway Data Plane
## Kong Mesh Control Plane
## Kong Mesh Data Plane

# Both CP and DP on VMs (outside Red Hat Scope)