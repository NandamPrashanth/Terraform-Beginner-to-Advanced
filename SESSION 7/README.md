# Terraform SESSION 7

---

## 📚 Table of Contents

1. [Built-in Functions](#built-in-functions)  
2. [Conditionals](#conditionals)  
3. [Loops](#loops)  
   - [count](#count)  
   - [for_each](#for_each)  
4. [Dynamic Blocks](#dynamic-blocks)  
5. [References](#references)  

---

## Built-in Functions

Terraform has many **built-in functions** that help you manipulate data, like strings, numbers, lists, and maps.

### 🔹 Examples and Outputs:

```hcl
# String function
output "lower_name" {
  value = lower("HELLO")
}

# Number function
output "sum_example" {
  value = max(5, 10)
}

# List function
output "first_item" {
  value = element(["apple", "banana", "cherry"], 0)
}
````

**Expected Output:**

```text
lower_name = "hello"
sum_example = 10
first_item = "apple"
```

### 🔗 Official Docs:

[https://developer.hashicorp.com/terraform/language/functions](https://developer.hashicorp.com/terraform/language/functions)

---

## Conditionals

Terraform supports **conditional expressions** (like `if` statements) to choose between values.

### 🔹 Syntax:

```hcl
condition ? true_value : false_value
```

### 🔹 Example:

```hcl
variable "environment" {
  default = "dev"
}

output "instance_type" {
  value = var.environment == "prod" ? "t3.large" : "t3.micro"
}
```

**Expected Output:**

```text
instance_type = "t3.micro"
```

---

## Loops

Terraform allows repeating resources using **`count`** or **`for_each`**.

### count

* Simple loop to create multiple identical resources.

```hcl
resource "aws_instance" "web" {
  count         = 3
  ami           = "ami-0c5204531f799e0c6"
  instance_type = "t3.micro"
}
```

**Expected Resources Created:**

```text
aws_instance.web[0]
aws_instance.web[1]
aws_instance.web[2]
```

---

### for_each

* More flexible than `count`, especially for maps or sets of strings.

```hcl
variable "servers" {
  default = {
    app1 = "t3.micro"
    app2 = "t3.small"
  }
}

resource "aws_instance" "app" {
  for_each      = var.servers
  ami           = "ami-0c5204531f799e0c6"
  instance_type = each.value
}
```

**Expected Resources Created:**

```text
aws_instance.app["app1"]  -> instance_type = "t3.micro"
aws_instance.app["app2"]  -> instance_type = "t3.small"
```

---

## Dynamic Blocks

Dynamic blocks allow generating **nested blocks** dynamically, useful for resources with complex or repeated nested structures.

### 🔹 Example:

```hcl
variable "subnets" {
  default = ["10.0.1.0/24", "10.0.2.0/24"]
}

resource "aws_security_group" "example" {
  name = "example-sg"

  dynamic "ingress" {
    for_each = var.subnets
    content {
      from_port   = 80
      to_port     = 80
      protocol    = "tcp"
      cidr_blocks = [ingress.value]
    }
  }
}
```

**Expected Output:**

Terraform will create **two ingress rules**, one for each subnet:

```text
aws_security_group.example
  ingress[0].cidr_blocks = ["10.0.1.0/24"]
  ingress[1].cidr_blocks = ["10.0.2.0/24"]
```

---

## References

* Terraform Functions: [https://developer.hashicorp.com/terraform/language/functions](https://developer.hashicorp.com/terraform/language/functions)
* Terraform Conditionals: [https://developer.hashicorp.com/terraform/language/expressions/conditionals](https://developer.hashicorp.com/terraform/language/expressions/conditionals)
* Terraform `count` and `for_each`: [https://developer.hashicorp.com/terraform/language/meta-arguments/count](https://developer.hashicorp.com/terraform/language/meta-arguments/count)
* Terraform Dynamic Blocks: [https://developer.hashicorp.com/terraform/language/expressions/dynamic-blocks](https://developer.hashicorp.com/terraform/language/expressions/dynamic-blocks)

---
