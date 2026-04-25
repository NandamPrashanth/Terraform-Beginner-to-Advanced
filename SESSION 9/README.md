# Terraform SESSION 9

---

## 📚 Table of Contents

1. [Managing Dev/Stage/Prod](#managing-devstageprod)  
2. [Workspaces vs Separate State Files](#workspaces-vs-separate-state-files)  
3. [References](#references)  

---

## Managing Dev/Stage/Prod

In Terraform, it is common to have multiple environments like **development, staging, and production**.  

### 🔹 Approaches:

1. **Separate Folders/Configs**
   - Each environment has its own folder and configuration.
   - Each folder has a separate `terraform.tfstate`.

```

terraform/
├── dev/
├── stage/
└── prod/

````

2. **Shared Configuration with Variables**
- Same codebase is used for all environments.
- Pass environment-specific values through **variables**.

```hcl
variable "environment" {}
output "current_env" {
  value = var.environment
}
````

### 💡 Tip:

* Use **dev for testing**, **stage for QA**, and **prod for production deployments**.
* Keep **state files separate** to avoid accidental overwrites.

---

## Workspaces vs Separate State Files

Terraform provides two ways to manage multiple environments:

### 1. Workspaces

* Workspaces allow **multiple states** from the **same configuration**.
* Default workspace = `default`
* Create a new workspace:

```bash
terraform workspace new dev
terraform workspace select dev
```

* Output the current workspace:

```hcl
output "current_workspace" {
  value = terraform.workspace
}
```

**Pros:**

* Easy to switch environments
* Same codebase for all environments

**Cons:**

* Not ideal for drastically different environments

---

### 2. Separate State Files

* Each environment has **its own configuration folder** or **state file**.
* Example:

```
terraform/
├── dev/terraform.tfstate
├── stage/terraform.tfstate
└── prod/terraform.tfstate
```

**Pros:**

* Complete isolation of environments
* Safer for production deployments

**Cons:**

* Slightly more overhead to maintain multiple folders

---

## References

* Terraform Workspaces: [https://developer.hashicorp.com/terraform/language/state/workspaces](https://developer.hashicorp.com/terraform/language/state/workspaces)
* Terraform Managing Multiple Environments: [[https://developer.hashicorp.com/terraform/tutorials/state/workspaces](https://developer.hashicorp.com/terraform/tutorials/state/workspaces)](https://developer.hashicorp.com/terraform/cloud-docs/workspaces)

---
