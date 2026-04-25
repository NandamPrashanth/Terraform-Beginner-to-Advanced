# Terraform SESSION 10

---

## 📚 Table of Contents

1. [Logging (TF_LOG)](#logging-tf_log)  
2. [Common Errors](#common-errors)  
3. [Dependency Issues](#dependency-issues)  
4. [References](#references)  

---

## Logging (TF_LOG)

Terraform supports logging using the **TF_LOG environment variable**.  
It helps you **debug Terraform runs**.

### 🔹 How to Enable Logging

```bash
# Set logging level
export TF_LOG=DEBUG
terraform apply
````

### 🔹 Logging Levels

| Level | Description                |
| ----- | -------------------------- |
| TRACE | Most detailed logs         |
| DEBUG | Useful for troubleshooting |
| INFO  | Basic operational info     |
| WARN  | Warnings                   |
| ERROR | Only errors                |

### 🔹 Example Output:

```text id="tf-log-example"
2026-04-25T12:00:00.000Z [DEBUG] Provider configuration loaded
2026-04-25T12:00:00.001Z [INFO] Creating resource aws_instance.web
2026-04-25T12:00:01.000Z [ERROR] Failed to create resource: Invalid AMI ID
```

### 💡 Tip:

* Use `DEBUG` for troubleshooting errors.
* Use `TRACE` for deep investigation of Terraform internals.

---

## Common Errors

Here are some frequent Terraform errors and their causes:

| Error Message                             | Cause                               | Tip                                         |
| ----------------------------------------- | ----------------------------------- | ------------------------------------------- |
| `Error: Invalid AMI ID`                   | Incorrect AMI ID in AWS resource    | Verify the AMI ID exists and is correct     |
| `Error: Resource already exists`          | Resource with same name exists      | Use unique names or `terraform import`      |
| `Error: Invalid type`                     | Wrong variable type                 | Check variable type in `variables.tf`       |
| `Error: Reference to undeclared resource` | Using resource before it is defined | Ensure dependencies or order are correct    |
| `Error: Permission denied`                | Insufficient IAM or OS permissions  | Check AWS IAM policies or local permissions |

---

## Dependency Issues

Terraform automatically detects **resource dependencies** but sometimes you need to define them manually.

### 🔹 Implicit Dependencies

* Terraform detects references automatically:

```hcl id="dep-example-implicit"
resource "aws_instance" "web" {
  ami           = "ami-0c5204531f799e0c6"
  instance_type = "t3.micro"
  subnet_id     = aws_subnet.main.id
}
```

* `aws_instance.web` depends on `aws_subnet.main` because of `subnet_id` reference.

### 🔹 Explicit Dependencies

* Use `depends_on` for resources not referenced directly:

```hcl id="dep-example-explicit"
resource "aws_instance" "web" {
  ami           = "ami-0c5204531f799e0c6"
  instance_type = "t3.micro"

  depends_on = [
    aws_vpc.main
  ]
}
```
---

## References

* Logging with TF_LOG: https://developer.hashicorp.com/terraform/cli/config/environment-variables#tf_log
---
