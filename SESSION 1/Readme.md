# Terraform SESSION 1

# 📦 Infrastructure as Code (IaC)

## 📖 Table of Contents

* [What is Infrastructure as Code (IaC)?](#what-is-infrastructure-as-code-iac)
* [Imperative vs Declarative Approach](#imperative-vs-declarative-approach)
* [Benefits of Terraform](#benefits-of-terraform)
* [Terraform vs Other Tools](#terraform-vs-other-tools)

  * [Terraform vs Ansible](#terraform-vs-ansible)
  * [Terraform vs CloudFormation](#terraform-vs-cloudformation)
  * [Terraform vs Pulumi](#terraform-vs-pulumi)
* [When to Use What?](#when-to-use-what)
* [Conclusion](#conclusion)

---

## 🚀 What is Infrastructure as Code (IaC)?

Infrastructure as Code (IaC) is a DevOps practice where infrastructure (servers, networks, databases, load balancers, etc.) is managed and provisioned using code instead of manual processes.

Instead of clicking through cloud consoles or running manual commands, you define infrastructure in configuration files and deploy it automatically.

### 🔑 Key Concepts:

* **Automation** – No manual setup required
* **Consistency** – Same environment every time
* **Version Control** – Track changes like application code
* **Reusability** – Use templates across environments
* **Scalability** – Easily scale infrastructure up/down

### 🧾 Example (Manual vs IaC)

**Manual Approach:**

```bash
aws ec2 run-instances --image-id ami-123456 --instance-type t2.micro
```

**IaC Approach (Terraform):**

```hcl
resource "aws_instance" "example" {
  ami           = "ami-123456"
  instance_type = "t2.micro"
}
```

---

##  Imperative vs Declarative Approach

IaC tools generally follow two programming styles:

---

### Imperative Approach (HOW)

In the imperative model, you explicitly define **step-by-step instructions** to reach the desired state.

#### 📌 Example:

```bash
# Step-by-step instructions
1. Create server
2. Install nginx
3. Start nginx service
```

#### ✅ Characteristics:

* Focus on **how to achieve** the result
* Requires detailed instructions
* Greater control over execution
* Harder to maintain at scale

#### ❌ Drawbacks:

* Not inherently idempotent
* More error-prone
* Difficult to track state

---

### Declarative Approach (WHAT)

In the declarative model, you define the **desired end state**, and the tool determines how to achieve it.

#### 📌 Example:

```hcl
resource "aws_instance" "web" {
  ami           = "ami-123456"
  instance_type = "t2.micro"
}
```

#### ✅ Characteristics:

* Focus on **what you want**
* Automatically handles changes
* Idempotent (same result every time)
* Easier to maintain and scale

#### ❌ Drawbacks:

* Less low-level control
* Debugging can be abstracted

---

### 🔍 Comparison Table

| Feature     | Imperative     | Declarative     |
| ----------- | -------------- | --------------- |
| Focus       | How to do      | What to achieve |
| Control     | High           | Moderate        |
| Complexity  | High           | Lower           |
| Idempotency | Not guaranteed | Built-in        |
| Maintenance | Difficult      | Easier          |

---

## 🌍 Benefits of Terraform

Terraform is an open-source Infrastructure as Code tool developed by HashiCorp. It uses a declarative approach and supports multiple cloud providers.

### 🚀 Key Benefits:

### 1. 🌐 Multi-Cloud Support

* Works with AWS, Azure, Google Cloud, Kubernetes, and more
* Avoids vendor lock-in

---

### 2. 🧾 Declarative Configuration (HCL)

* Uses HashiCorp Configuration Language (HCL)
* Easy to read and write

---

### 3. 📊 State Management

* Maintains a **state file** to track infrastructure
* Helps detect changes and avoid conflicts

---

### 4. 🔍 Execution Plan

```bash
terraform plan
```

* Shows what will change before applying
* Prevents unexpected modifications

---

### 5. 🔁 Idempotency

* Running the same configuration multiple times produces the same result

---

### 6. 🧩 Modular Architecture

* Reusable modules for common infrastructure patterns
* Encourages DRY (Don't Repeat Yourself)

---

### 7. 🌍 Large Ecosystem

* Hundreds of providers and modules
* Strong community support

---

## ⚔️ Terraform vs Other Tools

---

## 🆚 Terraform vs Ansible

| Feature           | Terraform                   | Ansible                  |
| ----------------- | --------------------------- | ------------------------ |
| Tool Type         | Infrastructure Provisioning | Configuration Management |
| Approach          | Declarative                 | Mostly Imperative        |
| State Management  | Yes                         | No                       |
| Primary Use       | Create infrastructure       | Configure software       |
| Agent Requirement | Agentless                   | Agentless                |

### 🧠 Explanation:

* **Terraform** is used to provision infrastructure (VMs, networks, etc.)
* **Ansible** is used to configure software inside those machines

👉 They are often used **together**:

* Terraform → Creates servers
* Ansible → Installs software on them

---

## 🆚 Terraform vs CloudFormation

| Feature          | Terraform              | CloudFormation           |
| ---------------- | ---------------------- | ------------------------ |
| Cloud Support    | Multi-cloud            | AWS only                 |
| Language         | HCL                    | JSON / YAML              |
| State Management | Managed via state file | Managed by AWS           |
| Flexibility      | High                   | Limited to AWS ecosystem |

### 🧠 Explanation:

* **Terraform** is cloud-agnostic
* **CloudFormation** is deeply integrated with AWS

👉 Choose:

* Terraform → Multi-cloud strategy
* CloudFormation → AWS-only environments

---

## 🆚 Terraform vs Pulumi

| Feature        | Terraform   | Pulumi                        |
| -------------- | ----------- | ----------------------------- |
| Language       | HCL         | Python, TypeScript, Go, etc.  |
| Approach       | Declarative | Imperative + Declarative      |
| Flexibility    | Moderate    | Very high                     |
| Learning Curve | Easier      | Depends on programming skills |

### 🧠 Explanation:

* **Terraform** uses a domain-specific language (HCL)
* **Pulumi** uses real programming languages

👉 Choose:

* Terraform → Simplicity & standardization
* Pulumi → Advanced logic & flexibility

---

## 🧠 When to Use What?

| Scenario                   | Recommended Tool |
| -------------------------- | ---------------- |
| Multi-cloud infrastructure | Terraform        |
| AWS-only environment       | CloudFormation   |
| Server configuration       | Ansible          |
| Complex logic in IaC       | Pulumi           |

---

## 📚 Further Reading

* Terraform Documentation: https://developer.hashicorp.com/terraform
* AWS CloudFormation Docs: https://docs.aws.amazon.com/cloudformation/
* Ansible Docs: https://docs.ansible.com/
* Pulumi Docs: https://www.pulumi.com/docs/

---
