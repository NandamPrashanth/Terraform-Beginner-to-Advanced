# Terraform SESSION 11

---

## 📚 Table of Contents

1. [Remote Backends](#remote-backends)  
2. [Terraform Cloud & Enterprise](#terraform-cloud--enterprise)  
3. [Sentinel Policies](#sentinel-policies)  
4. [Drift Detection](#drift-detection)  
5. [Import Existing Infrastructure](#import-existing-infrastructure)  
6. [References](#references)  

---

## Remote Backends

A **backend** in Terraform defines where the **state file is stored**.

By default, Terraform stores state locally (`terraform.tfstate`), which is risky for teams.

### 🔹 Why Remote Backends?
- Centralized state storage
- Team collaboration
- Locking (prevents simultaneous changes)
- Better security

---

### 🔹 Example (S3 Backend)

```hcl id="backend-s3"
terraform {
  backend "s3" {
    bucket = "my-terraform-state"
    key    = "dev/terraform.tfstate"
    region = "ap-south-1"
  }
}
````

---

### 💡 Behavior:

* State file is stored in S3 instead of local machine
* Multiple users can safely collaborate
* Supports state locking (via DynamoDB)

---

## Terraform Cloud & Enterprise

Terraform Cloud and Enterprise provide **managed infrastructure automation platforms**.

### 🔹 Features:

* Remote state storage
* Team collaboration (RBAC)
* Policy enforcement
* Private module registry
* CI/CD integration

---

### 🔹 Workflow:

```text
Developer → Terraform Cloud → Provider (AWS/Azure/GCP)
```

---

### 💡 Example:

Instead of running locally:

```bash
terraform apply
```

Terraform Cloud runs it remotely after receiving code changes.

---

### 🔹 Key Difference:

| Feature            | Terraform CLI | Terraform Cloud |
| ------------------ | ------------- | --------------- |
| State storage      | Local         | Remote          |
| Collaboration      | Manual        | Built-in        |
| Policy enforcement | No            | Yes             |

---

## Sentinel Policies

Sentinel is a **policy-as-code framework** used in Terraform Enterprise/Cloud.

### 🔹 Purpose:

* Enforce rules before infrastructure is created
* Prevent non-compliant resources

---

### 🔹 Example Policy Logic:

```text
IF instance_type == "t2.micro"
THEN allow
ELSE deny
```

---

### 💡 Real Use Cases:

* Prevent public S3 buckets
* Restrict instance types
* Enforce tagging standards

---

### 🔹 Behavior:

* Runs **before `terraform apply`**
* Blocks non-compliant deployments

---

## Drift Detection

**Drift** happens when infrastructure changes outside Terraform.

Example:

* Someone manually changes AWS console settings
* Terraform state no longer matches real infrastructure

---

### 🔹 Detect Drift:

```bash
terraform plan
```

---

### 🔹 Example Output:

```text id="drift-example"
~ aws_instance.web
    instance_type = "t3.micro" -> "t3.small"
```

---

### 💡 Explanation:

* `~` means **modified outside Terraform**
* Terraform detects difference between state and real infrastructure

---

### 🔹 Fix Drift:

```bash
terraform apply
```

This will bring infrastructure back to desired state.

---

## Import Existing Infrastructure

Terraform allows you to bring **existing resources under management**.

---

### 🔹 Command:

```bash
terraform import aws_instance.web i-1234567890abcdef
```

---

### 🔹 Important Notes:

* Only updates **state file**, NOT code
* You must manually write matching `.tf` configuration

---

### 🔹 Workflow:

```text
Existing Infra → terraform import → state file → write config → terraform apply
```

---

### 🔹 Example:

```hcl id="import-example"
resource "aws_instance" "web" {
  ami           = "ami-0c5204531f799e0c6"
  instance_type = "t3.micro"
}
```

Then:

```bash
terraform import aws_instance.web i-1234567890abcdef
```

---

### 💡 Key Idea:

Import = “Tell Terraform: this resource already exists, start managing it”

---

## References

* Remote Backends: [https://developer.hashicorp.com/terraform/language/settings/backends](https://developer.hashicorp.com/terraform/language/settings/backends)
* Terraform Cloud: [https://developer.hashicorp.com/terraform/cloud-docs](https://developer.hashicorp.com/terraform/cloud-docs)
* Sentinel Policies: [https://developer.hashicorp.com/terraform/cloud-docs/policy-enforcement/sentinel](https://developer.hashicorp.com/terraform/cloud-docs/policy-enforcement/sentinel)
* Drift Detection: [https://developer.hashicorp.com/terraform/cli/commands/plan](https://developer.hashicorp.com/terraform/cli/commands/plan)
* Import Resources: [https://developer.hashicorp.com/terraform/cli/import](https://developer.hashicorp.com/terraform/cli/import)

---
