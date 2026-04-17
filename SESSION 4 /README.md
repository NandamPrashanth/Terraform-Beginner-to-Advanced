# Terraform SESSION4

## Table of Contents

1. [Introduction](#introduction)
2. [Input Variables](#input-variables)
3. [Variable Types and Defaults](#variable-types-and-defaults)
4. [.tfvars Files](#tfvars-files)
5. [Environment Variables](#environment-variables)
6. [Outputs](#outputs)
7. [Best Practices](#best-practices)
8. [Official Links](#official-links)

---

In Terraform, **variables** and **outputs** are used to make configurations **dynamic, reusable, and modular**.

* **Input variables** allow passing values to Terraform modules.
* **Outputs** let you get information about the infrastructure after deployment.

This session focuses on the ways to define variables, set defaults, provide values, and retrieve outputs.

---

## Input Variables

**Definition:**
Input variables are **placeholders** for values that can be provided when running Terraform, allowing configurations to be **dynamic**.

**Example:**

```hcl id="p1v0"
variable "region" {
  description = "AWS region to deploy resources"
}

provider "aws" {
  region = var.region
}
```

**Key Points:**

* Use `variable` blocks to declare a variable.
* Access the variable using `var.<variable_name>` syntax.
* Values can be provided via CLI, `.tfvars` files, or environment variables.

---

## Variable Types and Defaults

**Definition:**
Terraform supports **different types of variables** to ensure type safety and optional defaults.

**Types:**

* `string` – Single text value
* `number` – Integer or float
* `bool` – true/false
* `list(type)` – Ordered list of values
* `map(type)` – Key-value pairs
* `object` / `tuple` – Complex structures

**Example with default:**

```hcl id="pqr3nv"
variable "instance_type" {
  description = "Type of EC2 instance"
  type        = string
  default     = "t2.micro"
}
```

**Key Points:**

* Defaults make variables **optional**.
* Explicit types prevent accidental misuse.

---

## .tfvars Files

**Definition:**
`.tfvars` files store **variable values separately** from the main configuration, making it easy to manage multiple environments.

**Example (`terraform.tfvars`):**

```hcl id="k8m5yt"
region        = "us-west-2"
instance_type = "t3.small"
```

**Usage:**

```bash
terraform apply -var-file="terraform.tfvars"
```

**Key Points:**

* Good for **environment-specific values**.
* Keeps sensitive or environment-specific configs out of main code.

---

## Environment Variables

**Definition:**
Terraform can read variable values directly from **environment variables**.

**Syntax:**

```
TF_VAR_<variable_name>=<value>
```

**Example:**

```bash
export TF_VAR_region="us-east-1"
terraform apply
```

**Key Points:**

* Convenient for automation and CI/CD pipelines.
* Overrides default values or `.tfvars` if provided.

---

## Outputs

**Definition:**
Outputs let Terraform **expose information** about created resources after deployment.

**Example:**

```hcl id="v0p2ql"
output "instance_public_ip" {
  description = "The public IP of the EC2 instance"
  value       = aws_instance.example.public_ip
}
```

**Key Points:**

* Use outputs for **debugging or passing values to other modules**.
* Supports `sensitive = true` to hide secrets.

---

## Best Practices

* Always **type your variables**.
* Use **defaults** for optional variables.
* Keep environment-specific values in `.tfvars` files.
* Use outputs to **share key resource information**.
* Prefer environment variables for **CI/CD automation**.

---

## Official Links

* Terraform Input Variables: https://developer.hashicorp.com/terraform/language/values/variables
* Terraform Variable Types and Defaults: https://developer.hashicorp.com/terraform/language/values/variables#type-constraints
* Terraform .tfvars Files: https://developer.hashicorp.com/terraform/language/values/variables#variable-definitions-tfvars-files
* Terraform Environment Variables: https://developer.hashicorp.com/terraform/cli/config/environment-variables
* Terraform Outputs: https://developer.hashicorp.com/terraform/language/values/outputs

---


