---
title: PowerShell
date: 2020-11-25 18:28:43
background: bg-[#397fe4]
tags:
  - 脚本
  - windows
categories:
  - 编程
  - 操作系统
intro: 这是 PowerShell 脚本入门的快速参考备忘单。
plugins:
  - copyCode
---

## 基本命令

### 辅助命令

**_Powershell 的命令遵循动词-名词格式。_**

一些常见的动词：

| 动词    | 描述                                       |
| ------- | ------------------------------------------------- |
| Get     | 用于检索信息。                     |
| Set     | 用于配置或更改设置。             |
| New     | 用于创建对象的新实例。          |
| Remove  | 用于删除或移除项目。             |
| Invoke  | 用于执行特定操作。   |
| Start   | 用于启动进程或操作。          |
| Stop    | 用于停止或终止进程或操作。 |
| Enable  | 用于激活或启用功能。             |
| Disable | 用于停用或禁用功能。          |
| Test    | 用于执行测试或检查。                  |
| Update  | 用于更新或刷新数据或配置。 |

列出可用模块

```powershell
Get-Module --ListAvailable
```

列出可用的 cmdlet 和函数。

```powershell
Get-Command -Module ActiveDirectory
```

检索帮助

```powershell
Get-Help <cmd>
Get-Help <cmd> -Examples
Get-Help -Name Get-Process -Parameter Id
```

列出别名及其对应的 cmdlet 名称。

```powershell
Get-Alias | Select-Object Name, Definition
```

**Get-Member:** 显示对象的属性和方法。

```powershell
Get-Process | Get-Member
```

### 对象操作 {.col-span-2}

**Select-Object:** 从对象中选择特定属性或自定义其显示。

```powershell
Get-Process | Select-Object Name, CPU
```

**Where-Object:** 根据指定条件筛选对象。

```powershell
Get-Service | Where-Object { $PSItem.Status -eq 'Running' }
#或
Get-Service | ? { $_.Status -eq 'Running' }
```

**Measure-Object:** 计算对象属性的统计信息，如总和、平均值和计数。

```powershell
Get-Process | Measure-Object -Property WorkingSet -Sum
```

**ForEach-Object:** 对集合中的每个对象执行操作。（注意：以下命令将为当前目录中的文件/文件夹添加前缀）

```powershell
Get-ChildItem | ForEach-Object { Rename-Item $_ -NewName "Prefix_$_" }
```

**Sort-Object:** 按指定属性对对象进行排序。

```powershell
Get-ChildItem | Sort-Object Length -Descending
```

**Format-Table:** 将输出格式化为具有指定列的表。

```powershell
Get-Service | Format-Table -AutoSize  # ft 别名
```

**Format-List:** 将输出格式化为属性和值的列表。

```powershell
Get-Process | Format-List -Property Name, CPU  # fl 别名
```

### 文件系统 {.col-span-2}

```powershell
New-Item -path file.txt -type 'file' -value '内容'
New-Item -path file.txt -type 'dir'
Copy-Item <源路径> -destination <目标路径>
Move-Item -path  <源路径> -destination <目标路径>
Remove-Item <文件>
Test-Path <路径>
Rename-Item -path <路径> -newname <新名称>

# 使用 .NET 基础类库
[System.IO.File]::WriteAllText('test.txt', '')
[System.IO.File]::Delete('test.txt')

Get-Content -Path "test.txt"
Get-Process | Out-File -FilePath "processes.txt"# 输出到文件
Get-Process | Export-Csv -Path "processes.csv"  # 输出到 csv
$data = Import-Csv -Path "data.csv"             # 从 csv 导入
```

## 系统管理

### Windows Management Instrumentation (WMI) {.col-span-2}

```powershell
# 检索 BIOS 信息
Get-CimInstance -ClassName Win32_BIOS
# 检索有关本地连接的物理磁盘设备的信息
Get-CimInstance -ClassName Win32_DiskDrive
# 检索有关已安装物理内存 (RAM) 的信息
Get-CimInstance -ClassName Win32_PhysicalMemory
# 检索有关已安装网络适配器（物理+虚拟）的信息
Get-CimInstance -ClassName Win32_NetworkAdapter
# 检索有关已安装显卡 (GPU) 的信息
Get-CimInstance -ClassName Win32_VideoController

# 列出所有类名
Get-CimClass | Select-Object -ExpandProperty CimClassName
# 浏览 root\cimv2 命名空间中可用的各种 WMI 类
Get-CimClass -Namespace root\cimv2
# 浏览 root\cimv2 命名空间下的子 WMI 命名空间
Get-CimInstance -Namespace root -ClassName __NAMESPACE
```

### 网络管理

```powershell
# 测试到远程主机的网络连接
Test-Connection -ComputerName google.com

# 检索网络适配器信息
Get-NetAdapter

# 检索 IP 地址信息
Get-NetIPAddress

# 检索路由表信息
Get-NetRoute

# 测试远程主机上的端口是否打开
Test-NetConnection google.com -Port 80
```

### 用户和组管理 {.col-span-2}

```powershell
# 检索本地用户帐户信息
Get-LocalUser

# 创建新的本地用户帐户
New-LocalUser -Name NewUser -Password (ConvertTo-SecureString "Password123" -AsPlainText -Force)

# 删除本地用户帐户
Remove-LocalUser -Name UserToRemove

# 检索本地组信息
Get-LocalGroup

# 将成员添加到本地组
Add-LocalGroupMember -Group Administrators -Member UserToAdd
```

### 安全和权限

```powershell
# 检索文件/目录的访问控制列表
Get-Acl C:\Path\To\File.txt

# 设置文件/目录的访问控制列表
Set-Acl -Path C:\Path\To\File.txt -AclObject $aclObject
```

### 注册表管理 {.col-span-2}

```powershell
# 检索注册表项值
Get-ItemProperty -Path "HKLM:\Software\Microsoft\Windows\CurrentVersion\Uninstall\*" | Select DisplayName, DisplayVersion

# 设置注册表项值
Set-ItemProperty -Path "HKLM:\Software\MyApp" -Name "SettingName" -Value "NewValue"

# 创建新的注册表项值
New-ItemProperty -Path "HKCU:\Software\MyApp" -Name "NewSetting" -Value "NewValue" -PropertyType String

# 删除注册表项值
Remove-ItemProperty -Path "HKCU:\Software\MyApp" -Name "SettingToRemove"

# 检查注册表项是否存在
Test-Path "HKLM:\Software\MyApp"
```

## 脚本编写

### 变量 {.col-span-2}

使用或不使用指定类型初始化变量：

```powershell
$var = 0
[int] $var = 'Trevor'         # (抛出异常)
[string] $var = 'Trevor'      # (不抛出异常)
$var.GetType()

# 多重赋值
$a,$b,$c = 'a','b','c'

# 创建数组
$arrayvar = @('va1','va2')

# 创建字典
$dict = @{k1 = 'test'; k2 = 'best'}
```

变量命令

```powershell
New-Variable -Name FirstName -Value Trevor
New-Variable FirstName -Value Trevor -Option <ReadOnly/Constant> #只读/常量

Get-Variable
Get-Variable | ? { $PSItem.Options -contains 'constant' }
Get-Variable | ? { $PSItem.Options -contains 'readonly' }

Remove-Variable -Name firstname
# 删除只读变量
Remove-Variable -Name firstname -Force
```

变量类型 int32, int64, string, bool

### 运算符

```powershell
# 运算符
# (a <op> b)

= , += / -= , ++ / --
-eq / -ne , -lt / -gt , -le / -ge  # 等于/不等于，小于/大于，小于等于/大于等于

$FirstName = 'Trevor'
$FirstName -like 'T*' # 模糊匹配
$true; $false #布尔值 true/false

# 三元运算符
$FoodToEat = $BaconIsYummy ? 'bacon' : 'beets'

# -notin 或 -in (不包含于/包含于)
'Celery' -in @('Bacon', 'Sausage', 'Steak')

# 输出: True
5 -is [int32] # 类型判断

# 正则表达式匹配，可以使用数组
'Trevor' -match '^T\w*'

# 查找多个匹配项。
$regex = [regex]'(\w*)'
$regex.Matches('this is test').Value
```

### 结构

#### I/O 操作

```powershell
"This displays a string" #这将显示一个字符串

Write-Host "color" -ForegroundColor Red #以红色前景输出 "color"

$age = Read-host "Enter age" #提示用户输入年龄

$pwd = Read-host "password" -asSecureString #以安全字符串形式提示用户输入密码

Clear-Host #清空控制台
```

####流程控制

```powershell
IF(<#条件#>){
<#命令#>}ELSEIF(){}ELSE{}

Switch($var){
  "val1"{<#命令#>; break}
    "val2"{<#命令#>; break}
}

For($ct=0;$ct -le 3;$ct++){}

ForEach($var in $arr){}

while($var -ne 0){}

Do{}While()
```

### 函数 / 模块 {.row-span-2}

#### 示例 1

```powershell
function funcname{

    [CmdletBinding()]
  param(
    [Parameter(Mandatory)] #必需参数
    [String]$user
  )
  Write-Host "welcome " $user #欢迎用户
    return "value" #返回值
}
$var = funcname -user pcb
```

#### 示例 2

```powershell
function Get-EvenNumbers {
    [CmdletBinding()]
    param (
        [Parameter(ValueFromPipeline = $true)] #接受管道输入
        [int] $Number
    )
    begin {<#命令#>} #开始块
    process { #处理块
        if ($Number % 2 -eq 0) {
            Write-Output $Number
        }
    }
    end {<#命令#>} #结束块
}
1..10 | Get-EvenNumbers
```

#### 模块

```powershell
# PowerShell 在以下路径中查找模块
$env:PSModulePath

# 列出系统上安装的所有模块
Get-Module -ListAvailable
# 导入到当前会话的模块
Get-Module

Import-Module <模块名>
Remove-Module <模块名>

Find-Module -Tag cloud #按标签查找模块
Find-Module -Name ps* #按名称查找模块

# 创建一个内存中的 PowerShell 模块
New-Module -Name trevor -ScriptBlock {
  function Add($a,$b) { $a + $b } }
```

### 提示

- 在大多数语言中，转义字符是反斜杠 **\\**，而在 PowerShell 中是反引号 **`**

```powershell

```

## 另请参阅 {.cols-1}

- [Microsoft PowerShell](https://learn.microsoft.com/zh-cn/powershell/scripting/samples/sample-scripts-for-administration?view=powershell-7.3)
  _(learn.microsoft.com)_
