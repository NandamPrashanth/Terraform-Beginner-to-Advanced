# Terraform SESSION 8

---

## 📚 Table of Contents

1. [null_resource](#null_resource)  
2. [local-exec](#local-exec)  
3. [remote-exec](#remote-exec)  
4. [References](#references)  

---

## null_resource

`null_resource` is a **special Terraform resource** that doesn’t manage real infrastructure.  
It’s used to trigger **provisioners** or **dependencies**.

### 🔹 Example:

```hcl id="null-example"
resource "null_resource" "example" {
  triggers = {
    always_run = timestamp()
  }
}
````

### 🔹 Explanation:

* `triggers` ensures the resource **runs every time** Terraform is applied
* Useful for running commands without a real resource

### 🔹 Expected Output:

```text
null_resource.example: Creating...
null_resource.example: Creation complete
```

---

## local-exec

`local-exec` runs **commands on the machine where Terraform runs** (your local machine).

### 🔹 Example:

```hcl id="local-exec-example"
resource "null_resource" "local" {
  provisioner "local-exec" {
    command = "echo Hello, Terraform!"
  }
}
```

### 🔹 Expected Output:

```text
null_resource.local: Creating...
Hello, Terraform!
null_resource.local: Creation complete
```

### 🔹 Notes:

* Runs locally on your system
* Can be used for scripts, notifications, or local setup

---

## remote-exec

`remote-exec` runs **commands on a remote machine**, typically via SSH.

### 🔹 Example:

```hcl id="remote-exec-example"
resource "aws_instance" "web" {
  ami           = "ami-0c5204531f799e0c6"
  instance_type = "t3.micro"
  key_name      = "my-key"

  provisioner "remote-exec" {
    inline = [
      "sudo apt-get update",
      "sudo apt-get install -y nginx"
    ]

    connection {
      type        = "ssh"
      user        = "ubuntu"
      private_key = file("~/.ssh/id_rsa")
      host        = self.public_ip
    }
  }
}
```

### 🔹 Expected Output:

```text
aws_instance.web: Creating...
aws_instance.web: Provisioning with 'remote-exec'...
aws_instance.web: Provisioning complete
```

### 🔹 Notes:

* Runs commands on remote instance after it’s created
* Requires **SSH access** and credentials

---

## References## References

- **null_resource**: [Terraform null_resource Documentation](https://registry.terraform.io/providers/hashicorp/null/latest/docs/resources/resource)  
- **Provisioners Overview**: [Terraform Provisioners Documentation](https://developer.hashicorp.com/terraform/language/provisioners)  
- **local-exec and remote-exec**: [Terraform Provisioners Documentation](https://developer.hashicorp.com/terraform/language/provisioners)
