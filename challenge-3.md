## Tasks

[1] Integrate with AAD to implement Role-Based Access Control (RBAC) for cluster authentication
[2] Protect your resources by using a dedicated VNet. Use the existing VNet in your subscription.
[3] Protect the most critical part of your Kubernetes cluster, the Kubernetes API Server.
    Only your team members should be able to access the Kubernetes API server.
[4] HA: It's important to consider the availability of the application (number of nodes in your cluster)
[5] Pods on your cluster should be able to directly communicate with other resources on the VNET via private IP addresses.


## Success Criteria
- Your team successfully created an RBAC enabled AKS cluster within the address space allocated to you by the network team
- Your team must demonstrate that you are prompted on cluster access to authenticate with AAD
- Your team must demonstrate connectivity to and from your cluster by being able to reach the internal-vm (already deployed)


## Testing

### RBAC in k8s
These permissions can be scoped to a single namespace, or granted across the entire AKS cluster. With Kubernetes RBAC, you create roles to define permissions, and then assign those roles to users with role bindings.

Kubernetes RBAC is designed to work on resources within your AKS cluster, and Azure RBAC is designed to work on resources within your Azure subscription. With Azure RBAC, you create a role definition that outlines the permissions to be applied. A user or group is then assigned this role definition for a particular scope, which could be an individual resource, a resource group, or across the subscription.

Before you assign permissions to users with Kubernetes RBAC, you first define those permissions as a Role. Kubernetes roles grant permissions. There is no concept of a deny permission.

Roles are used to grant permissions within a namespace. If you need to grant permissions across the entire cluster, or to cluster resources outside a given namespace, you can instead use ClusterRoles.

A ClusterRole works in the same way to grant permissions to resources, but can be applied to resources across the entire cluster, not a specific namespace.

Once roles are defined to grant permissions to resources, you assign those Kubernetes RBAC permissions with a RoleBinding. If your AKS cluster integrates with Azure Active Directory, bindings are how those Azure AD users are granted permissions to perform actions within the cluster.

Role bindings are used to assign roles for a given namespace. This approach lets you logically segregate a single AKS cluster, with users only able to access the application resources in their assigned namespace. If you need to bind roles across the entire cluster, or to cluster resources outside a given namespace, you can instead use ClusterRoleBindings.

A ClusterRoleBinding works in the same way to bind roles to users, but can be applied to resources across the entire cluster, not a specific namespace. This approach lets you grant administrators or support engineers access to all resources in the AKS cluster.




To obtain a kubectl configuration context, a user can run the az aks get-credentials command. When a user then interacts with the AKS cluster with kubectl, they are prompted to sign in with their Azure AD credentials. 
