# Terraform SESSION 3

## Table of Contents

1. [Introduction](#introduction)
2. [Providers](#providers)
3. [Multi-Cloud Concept](#multi-cloud-concept)
4. [Resource Blocks](#resource-blocks)
5. [Data Sources](#data-sources)
6. [Best Practices](#best-practices)
7. [Official Links](#official-links)

---

## Providers

**Definition:**
A provider is a plugin in Terraform that interacts with a specific cloud service or API. Providers are responsible for understanding API interactions, exposing resources, and performing CRUD (Create, Read, Update, Delete) operations.

**Example:**

```hcl
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 5.0"
    }
  }
}

provider "aws" {
  region = "us-west-2"
}
```
- required_providers → Tells Terraform which provider plugin and version to use.
- provider → Tells Terraform how to connect to that provider (region, credentials, etc.).

**Key Points:**

* Every provider is responsible for a particular service (e.g., AWS, Azure, GCP).
* Providers define **resources** and **data sources** for a service.
* You can configure multiple providers in one Terraform configuration for multi-cloud setups.

**Best Practices:**

* Pin provider versions to avoid breaking changes.
* Use provider aliases for multi-region or multi-account setups.
* Authenticate securely using environment variables or secrets managers.

**Official Link:**
[Terraform Providers](https://developer.hashicorp.com/terraform/docs/providers)

---

| Constraint             | Syntax Example  | Mathematical Symbol | Mathematical Meaning | Explanation                                                          |
| ---------------------- | --------------- | ------------------- | -------------------- | -------------------------------------------------------------------- |
| Exact Version          | `= 5.0.1`       | `=`                 | = 5.0.1              | Only this exact version is allowed. No upgrades.                     |
| Greater Than           | `> 5.0`         | `>`                 | > 5.0                | Only versions strictly higher than 5.0. 5.0 is not included.         |
| Greater Than or Equal  | `>= 5.0`        | `≥`                 | ≥ 5.0                | Version 5.0 and anything higher is allowed.                          |
| Less Than              | `< 6.0`         | `<`                 | < 6.0                | Any version below 6.0 is allowed. 6.0 is excluded.                   |
| Less Than or Equal     | `<= 5.2`        | `≤`                 | ≤ 5.2                | Versions up to 5.2 are allowed (including 5.2).                      |
| Not Equal              | `!= 5.0.1`      | `≠`                 | ≠ 5.0.1              | All versions except 5.0.1 are allowed.                               |
| Range (Combination)    | `>= 5.0, < 6.0` | `≥ , <`             | ≥ 5.0 AND < 6.0      | Allows versions between 5.0 (inclusive) and 6.0 (exclusive).         |
| Pessimistic (`~> 5.0`) | `~> 5.0`        | Range Operator      | ≥ 5.0 AND < 6.0      | Allows all 5.x versions but blocks 6.x (safe major upgrade control). |
| Pessimistic (`~> 5.2`) | `~> 5.2`        | Range Operator      | ≥ 5.2 AND < 5.3      | Allows only patch updates within 5.2 (e.g., 5.2.1, 5.2.5).           |


## Multi-Cloud Concept

**Definition:**
Multi-cloud refers to managing infrastructure across multiple cloud providers (e.g., AWS, Azure, GCP) in a single Terraform workflow.

**Example Scenario:**
You may deploy an application where the database is on AWS RDS, compute instances on Azure VM, and storage on Google Cloud Storage. Terraform can handle all these providers in a unified configuration.

**Example:**

```hcl
provider "aws" {
  region = "us-west-2"
}

provider "google" {
  project = "my-gcp-project"
  region  = "us-central1"
}
```

**Key Points:**

* Use **provider aliases** for multiple accounts/regions.
* Keep provider configurations modular.
* Enables hybrid and distributed architectures.

**Best Practices:**

* Use modules for provider-specific resources to maintain separation of concerns.
* Maintain consistent naming conventions across clouds.
* Keep credentials secure and avoid hardcoding them.

**Official Link:**
[Terraform Multi-Cloud Strategy](https://developer.hashicorp.com/terraform/tutorials)

---

## Resource Blocks

**Definition:**
A resource block describes a component of your infrastructure. It defines what you want Terraform to create, update, or delete.

**Syntax:**

```hcl
resource "aws_instance" "example" {
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t2.micro"

  tags = {
    Name = "example-instance"
  }
}
```

**Key Points:**

* Each resource block has a **type** and a **name**.
* Attributes inside a resource block define its configuration.
* Terraform tracks the state of each resource in the state file.

**Best Practices:**

* Use meaningful names for resources.
* Keep resource definitions modular using Terraform modules.
* Avoid manual changes to resources outside Terraform.

**Official Link:**
[Terraform Resource Documentation](https://developer.hashicorp.com/terraform/docs/language/resources/syntax)

---

## Data Sources

**Definition:**
Data sources allow Terraform to read information from existing infrastructure or services. They do not create resources but fetch information that can be used by resource blocks.

**Example:**

```hcl
data "aws_ami" "ubuntu" {
  most_recent = true
  owners      = ["0123456"]
  filter {
    name   = "name"
    values = ["ubuntu/images/hvm-ssd/ubuntu-focal-20.04-amd64-server-*"]
  }
}
```

**Key Points:**

* Useful for referencing existing infrastructure.
* Enables dynamic configuration without hardcoding values.
* Can be combined with resource blocks for automation.

**Best Practices:**

* Use data sources to avoid hardcoding IDs or names.
* Minimize the number of data lookups to improve plan performance.
* Validate retrieved data using Terraform expressions.

**Official Link:**
[Terraform Data Sources](https://developer.hashicorp.com/terraform/docs/language/data-sources)

---

## Best Practices

* Always **version your Terraform and providers**.
* Use **modules** to organize and reuse code.
* Keep **state files secure**, especially in remote backends.
* Use **Terraform fmt** and **linting tools** to maintain consistent code style.
* Plan before applying changes using `terraform plan`.
* Document your infrastructure in `README.md` for clarity.

---

## Official Links

* [Terraform Documentation](https://developer.hashicorp.com/terraform/docs)
* [Terraform Providers](https://developer.hashicorp.com/terraform/docs/providers)
* [Terraform Resources](https://developer.hashicorp.com/terraform/docs/language/resources/syntax)
* [Terraform Data Sources](https://developer.hashicorp.com/terraform/docs/language/data-sources)
* [Terraform Best Practices](https://developer.hashicorp.com/terraform/tutorials)

---
