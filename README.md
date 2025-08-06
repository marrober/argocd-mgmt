# Create the argocd instance using the command : 

````bash
oc apply -k pacman-01/config/
````

## Get the route and secret :

````bash
oc get route/pacman-01-argocd-server  -n pacman-01-argocd -o jsonpath='{"https://"}{.spec.host}{"\n"}'
oc get secret/pacman-01-argocd-cluster -n pacman-01-argocd -o jsonpath='{.data.admin\.password}'| base64 -d 
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