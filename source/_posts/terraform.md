---
title: Terraform
date: 2024-4-18
background: bg-[#7345b6]
tags:
  - container
  - virtual
categories:
  - 编程
intro: |
  这是一个 [Terraform](https://docs.docker.com/get-started/) 的快速参考备忘单。
plugins:
  - copyCode
---

## HCL 语法：{.cols-2}

```
(块名称)    (资源类型)    (资源名称)
    |           |             |
    ▽           ▽             ▽
resource "aws_instance" "my_aws_server" {
                                        --
    ami           = "ami-1251351351513"  |<--(参数)
    instance_type = "t2.micro"           |
                                        --

}

```

### 变量类型

- 简单类型：number, string, bool, null。

- 复杂类型：集合类型：list, map, set 结构类型：`object({<键> = <类型>, ...})`,
  `tuple([<类型>, ...])`

优先级顺序：defaults < 环境变量 < terraform.tfvars 文件 < terraform.tfvars.json 文件 < .auto.tfvars < 命令行
(-var & -var-file)

```
variable "<变量名>" {
    description = "<变量描述>"
    type        = <变量类型>
    default     = <默认值>
}

# 类型 string
variable "aws_region" {
    description = "AWS 区域"
    type        = string
    default     = "us-east-1"
}

# 类型 list(string)
variable "azs" {
    description = "区域中的可用区"
    type        = list(string)
    default     = [ "us-east-1a", "us-east-1b", "us-east-1c"]
}

# 类型 map
variable "amis" {
    type = map(string)
    default = {
      "eu-west-1" = "ami-0fdke15151513145",
      "us-east-1" = "ami-0d17359173587519"
    }
}

# 类型 object
variable "egress_dsg" {
    type = object({
        from_port = number
        to_port = number
        protocol = string
        cidr_blocks = list(string)
    })
    default = {
     from_port = 0,
     to_port = 65365,
     protocol = "tcp",
     cidr_blocks = ["100.0.0.0/16", "200.0.0.0/16", "0.0.0.0/0"]
    }
}
```

## 元参数

### 循环

count, for_each, [for( o in var.list: o.id])

```
# 使用 count 创建多个 EC2 实例
resource "aws_instance" "server" {
  ami = "ami-06ec8443c2a35b0ba"
  instance_type = "t2.micro"
  count = 3  # 创建 3 个资源
}

# 声明一个变量
variable "users" {
  type = list(string)
  default = ["demo-user", "admin1", "john"]
}

# 使用 for_each 创建 IAM 用户
resource "aws_iam_user" "test" {
  for_each = toset(var.users) # 将列表转换为集合
  name = each.key
}

# for 表达式通过转换另一个复杂类型值来创建一个复杂类型值。
variable "names" {
    type = list
    default = ["som", "john", "mary"]
}

output "show_names" {
    # 类似于 Python 的列表推导式
    value = [for n in var.names : upper(n)]
}

output "short_upper_names" {
  # 通过指定条件过滤结果列表：
  value = [for name in var.names : upper(name) if length(name) > 7]
}
```

### Splat 表达式

`Splat(var.list[*].id)`

```
# 启动一个 EC2 实例
resource "aws_instance" "server" {
  ami = "ami-05cafdf7c9f772ad2"
  instance_type = "t2.micro"
  count = 3
}

output "private_addresses"{
  value = aws_instance.server[*].private_ip  # splat 表达式
}
```

### depends_on

如果两个资源相互依赖，depends_on 指定该依赖关系以强制执行顺序

```
resource "aws_iam_role_policy" "example" {
    name = "example"
    role = "s3 access"
    policy = jsonencode({
      "Statement" = [{
        "Action" = "s3:*",
        "Effect" = "Allow",
      }],
    })
}

resource "aws_instance" "my_server" {
    ami  = "ami-a255235"
    instance_type = "t2.micro"

    iam_instance_profile = aws_iam_instance_profile.my_server

    depends_on = [
      aws_iam_role_policy.example,
    ]
```

### lifecycle

一组用于控制特定资源行为的元参数

```
resources "aws_instance" "server" {
  ami           = "ami-a1b3414"
  instance_type = "t2.micro"

  lifecycle {
    create_before_destroy = true
    ignore_changes = [
      # 某些资源具有元数据
      # 在 TF 外部自动修改

      tags
    ]
  }
}
```

### 条件表达式

`condition ? true_val : false_val`

### 内置函数

| 函数                                     | 结果                    |
| ------------------------------------------ | ----------------------- |
| `max(5, 10, 9)`                            | 12                      |
| `min(5, 10, 9)`                            | 5                       |
| `format("There are %d servers", 4)`        | There are 4 lights      |
| `join("," ["foo", "bar", "baz"])`          | foo,bar,baz             |
| `split(",", "foo,bar,baz")`                | `["foo", "bar", "baz"]` |
| `replace("hi world", "/w.*d/", "mom"`      | hi mom                  |
| `substr("hello world", 1, 4)`              | ello                    |
| `lookup({a="lol", b="sad"}, "a", "what?")` | lol                     |
| `lookup({a="lol", b="sad"}, "c", "what?")` | what?                   |
| `slice(["a", "b", "c", "d"], 1, 3)`        | `["b", "c"]`            |
| `timestamp()`                              | "2022-04-02T05:52:48Z"  |
| `cidr("10.1.2.240/28", 1)`                 | 10.1.2.241              |
| `cidr("10.1.2.240/28", 14)`                | 10.1.2.254              |

### Provider 块

正在使用的提供程序的详细信息。包括访问机制、区域选项、要使用的配置文件等信息。

```
provider "aws" {
  region = "us-east-1"
}

# 附加的提供程序配置引用为 `aws.west`。
provider "aws" {
  alias  = "west"
  region = "us-west-2"
}
```

### 请求提供程序

```
terraform {

  # required_providers 块指定源和版本
  required_providers {
    aws = {
      source  = "hashicorp/aws" # 在哪里找到提供程序
      version = "5.8.0" # 此配置需要哪个版本的提供程序
    }
  }
}
```

### Locals 块

本地值为表达式分配一个名称，因此您可以在模块中多次使用该名称，而不是重复表达式

```
locals {
  service_name = "forum"
  owner        = "Community Team"
}

# 一旦声明了 local，就可以引用它
locals {
  common_tags = {
    Service = local.service_name
    Owner   = local.owner
```

### Output 块

```
output "api_base_url" {
  value = "https://${aws_instance.example.private_dns}:8433/"

  # EC2 实例必须具有加密的根卷。
  precondition {
    condition     = data.aws_ebs_volume.example.encrypted
    error_message = "服务器的根卷未加密。"
  }

  # 输出可以标记为包含敏感信息
  sensitive = true # 输出可以标记为包含敏感信息
}
```

### Data 块

可以查询的数据源（云提供商、本地列表等）

```
data "aws_ami" "example" {
  most_recent = true

  owners = ["self"]
  tags = {
    Name   = "app-server"
    Tested = "true"
  }
}
```

### 模块

```
module "myec2" {
  source = "../modules/ec2"

  # 模块输入
  ami_id = var.ami_id
  instance_type = var.instance_type
  servers = var.servers
}
```

### 后端

后端定义了 Terraform 存储其状态数据文件的位置。

可用后端：local(默认), remote, azurerm, consul, cos, gcs, http, Kubernetes, oss, pg, s3

```
terraform {
  backend "remote" {
    organization = "example_corp"

    workspaces {
      name = "my-app-prod"
    }
  }
}
```

### 资源寻址

| 示例                                            | 描述                 |
| ------------------------------------------------- | -------------------- |
| `[模块路径][资源信息]`                             | 资源路径语法         |
| `module.<模块路径>[可选] 模块索引`                  | 模块路径语法         |
| `资源类型.用户定义名称[可选索引]`                    | 资源规范语法         |
| `<资源类型>.<名称>`                               | 列出所有镜像         |
| `var.<名称>`                                      | 输入变量             |
| `local.<名称>`                                    | 本地变量             |
| `module.<模块名称>`                               | 子模块输出           |
| `data.<数据类型>.<名称>`                            | 数据块               |
| `path.module`                                     | 表达式的位置         |
| `path.root`                                       | 根模块位置           |
| `terraform.workspace`                             | 当前工作区           |

---

## Terraform CLI

<!-- 我不知道这是什么意思，但它不适合某个类别并且会破坏内容 -->
<!-- 我把它注释掉了... -->

<!-- 创建/编辑 TF 配置文件 -> init -> plan -> validate -> apply -> destroy -->

### 初始化

```sh
terraform init [选项]

    -upgrade            # 安装最新的模块和提供程序版本
    -reconfigure        # 重新配置后端，忽略任何已保存的配置
    -backend=false      # 禁用后端并使用先前的初始化
    -migrate-state      # 重新配置后端并尝试迁移任何现有状态
```

### 计划

生成并审查执行计划

```sh
terraform plan [选项]

    -var 'user=john'    # 为配置的根模块中的输入变量设置值
    -var-file=filename  # 从给定文件加载变量值
    -input=true         # 如果未直接设置，则请求输入变量
    -out=path           # 将计划文件写入给定路径。可用作 "apply" 的输入
    -refresh-only       # 验证远程对象的一致性，而不建议执行操作来撤消在 TF 外部所做的更改
    -destroy            # 创建计划以销毁当前管理的所有对象
    -target=resource    # 仅将计划目标限定为给定资源及其依赖项。

terraform plan -refresh-only # 更新状态以匹配在 TF 外部所做的更改。适用于漂移检测

```

### 验证

```sh
terraform validate      # 验证配置文件是否存在错误

```

### 应用

执行对基础架构的更改

```sh
terraform apply [选项]

    -auto-approve       # 在应用前跳过计划的交互式批准
    -replace            # 强制替换特定资源实例
    -var 'foo=bar'      # 为配置的根模块中的输入变量设置值
    -var-file=filename  # 从给定文件加载变量值
    -parallelism=n      # 限制并发操作的数量。默认=10

terraform apply -auto-approve var-file=web-dev.tfvars
terraform apply -replace="aws_instance.server"
terraform plan -refresh-only # 更新状态文件以接受手动进行的更改。
```

### 销毁

销毁（删除）Terraform 管理的基础架构。与 `terraform apply -destroy` 相同

```sh
terraform destroy [选项]

    -auto-approve        # 在销毁前跳过交互式批准
    -target              # 仅将销毁限制为给定资源及其依赖项


terraform destroy -target aws_vpc.my_vpc -auto-approve
```

杂项

```sh
terraform state show aws_instance.my_vm
terraform state pull > my_terraform.tfstate
terraform state mv aws_iam_role.my_ssm_role
terraform state list
terraform state rm aws_instance.my_server

terraform import aws_instance.new_server i-243abc
sudo apt install graphviz
terraform graph | dot -Tpng > graph.png
```

日志记录

日志级别 = TRACE > DEBUG > INFO > WARN > ERROR

```sh
export TF_LOG_CORE=TRACE     # 启用核心日志记录
export TF_LOG_PROVIDER=TRACE # 启用提供程序日志记录
export TF_LOG_PATH=logs.txt  # 持久化日志
```

## 另请参阅

- [文档](https://developer.hashicorp.com/terraform/language)
- [不错的 FCC 文章](https://www.freecodecamp.org/news/terraform-certified-associate-003-study-notes/)

