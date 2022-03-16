# Pod Security Policies  

This Repo includes yaml files to apply security for kubernetes cluster  
To enable PSPs on a cluster, an admission plugin needs to be enabled, which can be done by adding:  
`PodSecurityPolicy` to the list of plugins stated by the flag `--enabled-admission-plugins`  

for example:  
`--enable-admission-plugins=NamespaceLifecycle,LimitRanger,ServiceAccount,DefaultStorageClass,DefaultTolerationSeconds,MutatingAdmissionWebhook,ValidatingAdmissionWebhook,ResourceQuota,PodSecurityPolicy`

Using service accounts is needed, so the following flag can be added to kubernetes command args as well:  
`--use-service-account-credentials=true`  

### Applying YAML files to the cluster

After preparations was done,the configurations can be applied in the cluster  
We apply objects from those kinds, in the following order:  

#### 1. PodSecurityPolicies directory
Those are the PSPs that will be referenced from the ClusterRoles that we will apply

#### 2. ClusterRoles directory
Those will be the roles we will create to apply the rules we state

#### 3. RoleBindings and ClusterRoleBindings directories
Those will be the bindings to the "subject" that we state, that the roles will be applied to

To apply each directory of YAMLs, run the following commands:  
`kubectl apply -k ./PodSecurityPolicies`  
`kubectl apply -k ./ClusterRoles`  
`kubectl apply -k ./RoleBindings`  
`kubectl apply -k ./ClusterRoleBindings`  