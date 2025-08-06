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
oc get route/pacman-02-argocd-server  -n pacman-02-argocd -o jsonpath='{"https://"}{.spec.host}{"\n"}'
oc get secret/pacman-02-argocd-cluster -n pacman-02-argocd -o jsonpath='{.data.admin\.password}'| base64 -d 
echo ""
````

pacman-03

````bash
oc get route/pacman-03-argocd-server  -n pacman-03-argocd -o jsonpath='{"https://"}{.spec.host}{"\n"}'
oc get secret/pacman-03-argocd-cluster -n pacman-03-argocd -o jsonpath='{.data.admin\.password}'| base64 -d 
echo ""
````

## Tidy up projects

oc delete project pacman-01-argocd
oc delete project pacman-02-argocd
oc delete project pacman-03-argocd
oc delete project pacman-01-dev-01
oc delete project pacman-01-dev-02
oc delete project pacman-02-dev-01
oc delete project pacman-02-dev-02
oc delete project pacman-03-dev-01
oc delete project pacman-03-dev-02