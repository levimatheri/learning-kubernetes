## Creating AKS cluster ##
`az aks create --resource-group glowingwafflerg --name glowingwaffleaks --node-count 2 --enable-addons monitoring --generate-ssh-keys --windows-admin-username glowingadmin --vm-set-type VirtualMachineScaleSets --network-plugin azure`

## Get AKS cluster credentials ##
`az aks get-credentials --resource-group glowingwafflerg --name glowingwaffleaks`