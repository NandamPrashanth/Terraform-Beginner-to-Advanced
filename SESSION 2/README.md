# Terraform SESSION2 

# 📦 Installation & Workflow

## 📖 Table of Contents

* [Introduction](#introduction)
* [Terraform Installation](#terraform-installation)
* [Terraform Workflow](#terraform-workflow)

  * [terraform init](#terraform-init)
  * [terraform plan](#terraform-plan)
  * [terraform apply](#terraform-apply)
  * [terraform destroy](#terraform-destroy)
* [Understanding .tf Files](#understanding-tf-files)
* [Basic Example](#basic-example)
* [Conclusion](#conclusion)

---

## 🚀 Introduction

In this session, we will cover:

* How to install Terraform
* The complete Terraform workflow
* Core commands used in real-world projects
* Understanding `.tf` configuration files

---

## ⚙️ Terraform Installation

Terraform is a CLI-based tool, so installation is straightforward.

### 🖥️ Step 1: Download Terraform

* Visit: https://developer.hashicorp.com/terraform/downloads
* Choose your operating system (Windows, Linux, macOS)

---

### 🧰 Step 2: Install

#### 🔹 On Linux / macOS:

```bash
# Download and unzip
wget https://releases.hashicorp.com/terraform/<version>/terraform_<version>_linux_amd64.zip
unzip terraform_<version>_linux_amd64.zip

# Move to PATH
sudo mv terraform /usr/local/bin/
```

#### 🔹 On Windows:

1. Download ZIP file
2. Extract it
3. Add the folder path to **Environment Variables (PATH)**

---

### ✅ Step 3: Verify Installation

```bash
terraform -version
```

---

## 🔄 Terraform Workflow

Terraform follows a standard workflow for provisioning infrastructure.

### 📊 Workflow Steps:

1. Write configuration (`.tf` files)
2. Initialize project → `terraform init`
3. Preview changes → `terraform plan`
4. Apply changes → `terraform apply`
5. Destroy resources → `terraform destroy`

---

## 🔹 terraform init

### 📌 Purpose:

Initializes a Terraform working directory.

### What it does:

* Downloads required providers (AWS, Azure, etc.)
* Sets up backend (state storage)
* Prepares the project for execution

### 💻 Command:

```bash
terraform init
```

### 🧠 When to use:

* First time running Terraform in a directory
* After adding new providers or modules

---

## 🔹 terraform plan

### 📌 Purpose:

Creates an execution plan showing what changes Terraform will make.

### What it does:

* Compares current state vs desired configuration
* Shows resources to be created, modified, or destroyed

### 💻 Command:

```bash
terraform plan
```

### 📊 Example Output:

```bash
+ create aws_instance.example
~ update aws_security_group.sg
- destroy aws_s3_bucket.old
```

### 🧠 Why it's important:

* Prevents unexpected changes
* Acts as a safety check before deployment

---

## 🔹 terraform apply

### 📌 Purpose:

Applies the changes required to reach the desired state.

### 💻 Command:

```bash
terraform apply
```

### What it does:

* Executes the plan
* Creates/updates infrastructure
* Updates the state file

### ⚠️ Confirmation:

Terraform will ask:

```bash
Do you want to perform these actions?
```

You must type:

```bash
yes
```

### 🚀 Auto-approve option:

```bash
terraform apply -auto-approve
```

---

## 🔹 terraform destroy

### 📌 Purpose:

Deletes all resources managed by Terraform.

### 💻 Command:

```bash
terraform destroy
```

###  What it does:

* Removes infrastructure
* Updates state file accordingly

### ⚠️ Warning:

* This is irreversible
* Always double-check before running

### 🚀 Auto-approve:

```bash
terraform destroy -auto-approve
```

---

## 📄 Understanding .tf Files

Terraform uses `.tf` files to define infrastructure.

---

### 📌 What are `.tf` files?

* Text files written in **HCL (HashiCorp Configuration Language)**
* Contain resource definitions, variables, outputs, etc.

---

### 🧱 Common Types of `.tf` Files

| File Name    | Purpose                           |
| ------------ | --------------------------------- |
| main.tf      | Main infrastructure configuration |
| variables.tf | Input variables                   |
| outputs.tf   | Output values                     |
| provider.tf  | Provider configuration            |

---

### 🧾 Example `.tf` File

```hcl
provider "aws" {
  region = "us-east-1"
}

resource "aws_instance" "web" {
  ami           = "ami-123456"
  instance_type = "t2.micro"
}
```

---

### 🧠 Key Blocks in `.tf` Files

#### 🔹 Provider Block

Defines the cloud provider:

```hcl
provider "aws" {
  region = "us-east-1"
}
```

#### 🔹 Resource Block

Defines infrastructure:

```hcl
resource "aws_instance" "example" {
  ami           = "ami-123456"
  instance_type = "t2.micro"
}
```

#### 🔹 Variable Block

```hcl
variable "instance_type" {
  default = "t2.micro"
}
```

#### 🔹 Output Block

```hcl
output "instance_ip" {
  value = aws_instance.example.public_ip
}
```

---

## Basic Example

### 📁 Project Structure:

```
terraform-project/
│── main.tf
```

### 📄 main.tf:

```hcl
provider "aws" {
  region = "us-east-1"
}

resource "aws_instance" "demo" {
  ami           = "ami-123456"
  instance_type = "t2.micro"
}
```

---

### ▶️ Execution Steps:

```bash
terraform init
terraform plan
terraform apply
```

---

### 🧹 Cleanup:

```bash
terraform destroy
```

---

## 📚 Best Practices

* Always use version control (Git)
* Never commit sensitive data
* Use variables for flexibility
* Review plans before applying
* Use remote state for team collaboration

---
