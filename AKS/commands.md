## Creating AKS cluster ##
`az aks create --resource-group glowingwafflerg --name glowingwaffleaks --node-count 2 --enable-addons monitoring --generate-ssh-keys --windows-admin-username glowingadmin --vm-set-type VirtualMachineScaleSets --network-plugin azure`

## Get AKS cluster credentials ##
`az aks get-credentials --resource-group glowingwafflerg --name glowingwaffleaks`

## Add Windows node pool ##
`az aks nodepool add --resource-group glowingwafflerg --cluster-name glowingwaffleaks --os-type Windows --name npwin --node-count 1 --aks-custom-headers WindowsContainerRuntime=containerd`

## Add Linux node pool ##
`az aks nodepool add --resource-group glowingwafflerg --cluster-name glowingwaffleaks --name mynodepool --node-count 2`

## Install nginx ingress controller ##
```
helm install nginx-ingress ingress-nginx/ingress-nginx `
    --namespace ingress `
    -f internal-ingress.yaml `
    --set controller.replicaCount=2 `
    --set controller.nodeSelector."beta\.kubernetes\.io/os"=linux `
    --set defaultBackend.nodeSelector."beta\.kubernetes\.io/os"=linux `
    --set controller.admissionWebhooks.patch.nodeSelector."beta\.kubernetes\.io/os"=linux
```