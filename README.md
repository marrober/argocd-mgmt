# Create the argocd instance using the command : 

````bash
oc apply -k pacman-01/config/
````

## Get the route and secret :

pacman-01

````bash
oc get route/pacman-01-server  -n pacman-01-argocd -o jsonpath='{"https://"}{.spec.host}{"\n"}'
oc get secret/pacman-01-cluster -n pacman-01-argocd -o jsonpath='{.data.admin\.password}'| base64 -d 
echo ""
````

pacman-02

````bash
oc get route/pacman-02-server  -n pacman-02-argocd -o jsonpath='{"https://"}{.spec.host}{"\n"}'
oc get secret/pacman-02-cluster -n pacman-02-argocd -o jsonpath='{.data.admin\.password}'| base64 -d 
echo ""
````

pacman-03

````bash
oc get route/pacman-03-server  -n pacman-03-argocd -o jsonpath='{"https://"}{.spec.host}{"\n"}'
oc get secret/pacman-03-cluster -n pacman-03-argocd -o jsonpath='{.data.admin\.password}'| base64 -d 
echo ""
````

## Tidy up projects

oc delete application.argoproj.io/pacman-01-dev-01 -n pacman-01-argocd
oc delete application.argoproj.io/pacman-01-dev-02 -n pacman-01-argocd
oc delete application.argoproj.io/pacman-01-dev-03 -n pacman-01-argocd
oc delete application.argoproj.io/pacman-02-dev-01 -n pacman-01-argocd
oc delete application.argoproj.io/pacman-02-dev-02 -n pacman-02-argocd
oc delete application.argoproj.io/pacman-03-dev-01 -n pacman-03-argocd
oc delete application.argoproj.io/pacman-03-dev-02 -n pacman-03-argocd
oc delete application.argoproj.io/pacman-01-root -n pacman-01-argocd
oc delete application.argoproj.io/pacman-02-root -n pacman-02-argocd
oc delete application.argoproj.io/pacman-03-root -n pacman-03-argocd
oc delete application.argoproj.io/app-in-namespace-root -n openshift-gitops
oc delete application.argoproj.io/pacman-01 -n openshift-gitops
oc delete application.argoproj.io/pacman-02 -n openshift-gitops
oc delete application.argoproj.io/pacman-03 -n openshift-gitops
oc delete application.argoproj.io/index-management -n openshift-gitops

oc delete project pacman-01-argocd
oc delete project pacman-02-argocd
oc delete project pacman-03-argocd
oc delete project pacman-01-dev-01
oc delete project pacman-01-dev-02
oc delete project pacman-01-dev-03
oc delete project pacman-02-dev-01
oc delete project pacman-02-dev-02
oc delete project pacman-03-dev-01
oc delete project pacman-03-dev-02

oc delete appproject/app-in-namespace-root -n openshift-gitops