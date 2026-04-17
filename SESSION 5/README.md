# Terraform SESSION 5

---

## Table of Contents

1. [Introduction](#introduction)
2. [Terraform State](#terraform-state)
3. [Local vs Remote State](#local-vs-remote-state)
4. [State Locking](#state-locking)
5. [State File Structure](#state-file-structure)
6. [Best Practices](#best-practices)
7. [Official Links](#official-links)

---

Terraform keeps track of resources it manages using a **state file**.

* The state file acts as a **mapping between your configuration and real-world infrastructure**.
* Proper handling of state is crucial for safe and collaborative Terraform usage.

---

## Terraform State

**Definition:**
Terraform state is a **JSON file** that stores the current status of infrastructure resources managed by Terraform.

**Key Points:**

* Keeps track of **resource IDs, attributes, dependencies, and metadata**.
* Improves Terraform performance by avoiding repeated API calls.
* Enables **terraform plan** to detect changes accurately.

**Example:**
By default, the state is stored in a file called `terraform.tfstate`.

---

## Local vs Remote State

**Local State:**

* Stored on your local machine (`terraform.tfstate`).
* Suitable for **personal projects** or experimentation.
* Risky for teams because of **state conflicts**.

**Remote State:**

* Stored in **remote backends** (S3, Terraform Cloud, Azure Blob, GCS, etc.).
* Supports **collaboration** and **state locking**.
* Allows **versioning** and **history** of state.

**Example Remote Backend (AWS S3):**

```hcl id="rt92b8"
terraform {
  backend "s3" {
    bucket = "my-terraform-state"
    key    = "project/terraform.tfstate"
    region = "us-west-2"
  }
}
```

---

## State Locking

**Definition:**
State locking **prevents multiple users or processes from modifying the state simultaneously**.

**Key Points:**

* Avoids **race conditions and corrupted state**.
* Supported by most **remote backends** (e.g., S3 with DynamoDB, Terraform Cloud).

**Example (S3 with DynamoDB lock table):**

```hcl id="h0r9js"
terraform {
  backend "s3" {
    bucket         = "my-terraform-state"
    key            = "project/terraform.tfstate"
    region         = "us-west-2"
    dynamodb_table = "terraform-locks"
  }
}
```

---

## State File Structure

**Definition:**
The state file is a **JSON document** that stores:

* **Resources**: type, name, ID, attributes
* **Dependencies** between resources
* **Module hierarchy**

**Key Points:**

* Do **not edit the state file manually**.
* Sensitive information may be stored in plain text—handle securely.
* Terraform uses this file to **plan, apply, and destroy resources accurately**.

---

## Best Practices

* Use **remote state** for team projects.
* Enable **state locking** to avoid conflicts.
* Keep the state file **secure** (especially if sensitive data exists).
* Avoid manual edits; use `terraform state` commands instead.
* Enable **versioning** for remote state backends.

---

## Official Links

- Terraform State: [https://developer.hashicorp.com/terraform/language/state](https://developer.hashicorp.com/terraform/language/state)
- Local vs Remote State: [https://developer.hashicorp.com/terraform/language/state/remote](https://developer.hashicorp.com/terraform/language/state/remote)
- State Locking: [https://developer.hashicorp.com/terraform/language/state/locking](https://developer.hashicorp.com/terraform/language/state/locking)

---
