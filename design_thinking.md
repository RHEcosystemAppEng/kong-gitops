# Argo CD deployment (separate from automation)
    - 1st OpenShift (Argo CD and Kong CP)
    - 2nd OpenShift ()
    - operator deployment
    - Getting the password of UI
    - import the CP and DP clusters


# Kong Gateway Control Plane 
    - Pre-requisites
        - create ns for kong
    - Infra components
        - create license secret (first manually)
            - Then using hashicorp vault (In 2nd iteration) 
                - https://cloud.redhat.com/blog/how-to-use-hashicorp-vault-and-argo-cd-for-gitops-on-openshift
        - Generate cert + secret 
    -  Deploy control plane - use kustomize
        - Variation from what we have done? - For postgres, we need to use the postgres subchart from kong
        - Best practice - use helm values (cp-values.yaml)
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

# Kong Gateway Data Plane
    - Pre-requisites
        - same as above
    - Infra component
        - same as above
        - (+) - Keycloak server
    - Deploy data plane (using dp-values.yaml) - use kustomize
    - Post install of kong dp
    - validation
        - check clustering
        - any additional validation
    - Technical Notes
        - Order - dependent deployments (https://argo-cd.readthedocs.io/en/stable/user-guide/sync-waves/)
        - References
        - https://argo-cd.readthedocs.io/en/stable/

    

