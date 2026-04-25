# Terraform SESSION 6
---

## 📚 Table of Contents

1. [What are Modules](#what-are-modules)
2. [Root vs Child Modules](#root-vs-child-modules)
3. [Module Structure](#module-structure)
4. [Terraform Registry](#terraform-registry)
5. [References](#references)

---

## What are Modules

**Modules** in Terraform are reusable pieces of code.

Instead of writing the same configuration again and again, you can create a module once and reuse it multiple times.

### 💡 Simple Idea:

A module is just a **folder that contains Terraform code**.

### ✅ Why use modules?

* Avoid repeating code
* Keep code clean and organized
* Make infrastructure reusable

### 📦 Example:

If you need multiple servers with the same setup, create one module and reuse it.

### 🔗 Official Docs:

[https://developer.hashicorp.com/terraform/language/modules](https://developer.hashicorp.com/terraform/language/modules)

---

## Root vs Child Modules

### 🟢 Root Module

* The **main folder** where you run:

  ```bash
  terraform init
  terraform apply
  ```
* This is your **starting point**

### 🔵 Child Module

* A module that is **called inside another module**
* Used to break code into smaller reusable parts

### 💡 Simple Analogy:

* Root module = Main project
* Child module = Reusable components inside the project

### 📦 Example:

```hcl
module "ec2_instance" {
  source = "./modules/ec2"
}
```

### 🔗 Official Docs:

[https://developer.hashicorp.com/terraform/intro/getting-started/modules.html](https://developer.hashicorp.com/terraform/intro/getting-started/modules.html)

---

## Module Structure

A module is simply a **directory with `.tf` files**.

### 📁 Example Structure:

```
my-module/
├── main.tf
├── variables.tf
├── outputs.tf
└── README.md
```

### 📌 File Explanation:

* `main.tf` → Contains resources
* `variables.tf` → Input values
* `outputs.tf` → Output values
* `README.md` → Documentation (optional but recommended)

### 💡 Tip:

Keep modules **small and focused on one task**.

### 🔗 Official Docs:

[https://developer.hashicorp.com/terraform/intro/getting-started/modules.html](https://developer.hashicorp.com/terraform/intro/getting-started/modules.html)

---

## Terraform Registry

The **Terraform Registry** is a public platform where you can find ready-made modules.

### 🌐 What you can do:

* Search for modules
* Use verified modules
* Publish your own modules

### 💡 Simple Idea:

It’s like an **app store for Terraform modules**.

### 📦 Example:

```hcl
module "vpc" {
  source  = "terraform-aws-modules/vpc/aws"
  version = "3.0.0"

  name = "my-vpc"
  cidr = "10.0.0.0/16"
}
```

### 🔗 Visit Registry:

[https://registry.terraform.io/](https://registry.terraform.io/)

---

## 📚 References

* Terraform Modules Overview
  [https://developer.hashicorp.com/terraform/language/modules](https://developer.hashicorp.com/terraform/language/modules)

* Terraform Modules Getting Started
  [https://developer.hashicorp.com/terraform/intro/getting-started/modules.html](https://developer.hashicorp.com/terraform/intro/getting-started/modules.html)

* Terraform Registry
  [https://registry.terraform.io/](https://registry.terraform.io/)

* Using Modules from Registry
  [https://developer.hashicorp.com/terraform/tutorials/modules/module-use](https://developer.hashicorp.com/terraform/tutorials/modules/module-use)

---
