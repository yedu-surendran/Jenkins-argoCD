# Role-Based Access Control (RBAC) in ArgoCD

## Introduction to RBAC in ArgoCD

ArgoCD uses Role-Based Access Control (RBAC) to provide fine-grained permissions to users and manage access to applications and other resources. By creating roles with specific permissions, administrators can limit access to certain ArgoCD functions. In this lab, we'll demonstrate how to create a new user, define a custom role, and assign that role to the user.

## Prerequisites

- A running ArgoCD instance on Kubernetes.
- Access to `kubectl` configured for your Kubernetes cluster.
- Admin privileges in ArgoCD to edit `ConfigMaps` and define policies.

## Lab Steps

### Step 1: Download the ArgoCD CLI

The ArgoCD CLI provides command-line access to interact with the ArgoCD server. Download and install it with the following commands:

```bash
curl -sSL -o argocd-linux-amd64 https://github.com/argoproj/argo-cd/releases/download/v2.13.0/argocd-linux-amd64
sudo install -m 555 argocd-linux-amd64 /usr/local/bin/argocd
```

### Step 2: Log in to the ArgoCD Server

Using the CLI, log in to the ArgoCD server. Replace `<PublicIP:NodePort>` with the actual IP and port of your ArgoCD server:

```bash
argocd login <PublicIP:NodePort> --username admin --password ZjpgCFwuRfd2TKpU
```

### Step 3: List User Accounts

To view all user accounts in ArgoCD, use the following command:

```bash
argocd account list
```

This command will display a list of current user accounts and their associated roles.

### Step 4: Add a New User to ArgoCD

To create a new user in ArgoCD, edit the ArgoCD ConfigMap (`argocd-cm`). Run:

```bash
kubectl edit configmap argocd-cm -n argocd
```

Add the following under the `data` section to define a new user account:

```yaml
data:
  accounts.ninad: apiKey,login
```

This configuration creates a user named `ninad` and grants API key and login access.

### Update Passwords for Users

After creating the `ninad` user, you can set or update passwords for both the `admin` and `ninad` users using the ArgoCD CLI.

#### Update the Admin Password

To change the password for the `admin` user, run the following command:

```bash
argocd account update-password --account admin 
```

#### Set or Update the Password for the Ninad User

Similarly, set a password for the newly created `ninad` user:

```bash
argocd account update-password --account ninad 
```

### Step 5: Create an RBAC Policy for the New User

Define an RBAC policy and assign it to the `ninad` user. Edit the `argocd-rbac-cm` ConfigMap:

```bash
kubectl edit cm argocd-rbac-cm -n argocd
```

In the `data` section, add the following configuration to create a new role (`tester`) and assign it to `ninad`:

```yaml
data:
  policy.csv: |
    p, role:tester, applications, get, *, allow
    g, ninad, role:tester
```

This configuration creates a `tester` role with permissions to view (`get`) all applications. The second line assigns this `tester` role to the `ninad` user.

### Step 6: Verify the New User and RBAC Policy

Restart the ArgoCD server to apply the new configuration (optional but recommended for immediate effect).

To confirm the setup, try logging in as `ninad` and listing applications in ArgoCD to verify that the `tester` role's permissions are correctly applied.

