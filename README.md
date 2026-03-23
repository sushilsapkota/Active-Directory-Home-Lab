# 🏢 Active Directory Home Lab — Windows Server 2019

## Overview
Built a fully functional Active Directory environment from scratch on Windows Server 2019 to simulate a real enterprise IT environment. This lab mirrors tasks performed daily by IT Support Analysts and Systems Administrators.

---

## 🖥️ Environment
| Component | Details |
|---|---|
| OS | Windows Server 2019 |
| Domain | sushiit.local |
| Forest | sushiit.local |
| Domain Controller | WIN-E09DIUBB1HN |
| Tool | Active Directory Users & Computers |
| Policy Tool | Group Policy Management Console |

---

## 📁 OU Structure
```
sushiit.local
├── IT Departments
│   ├── John Smith (jsmith)
│   ├── Sarah Jones (sjones)
│   ├── IT-Admin (Security Group)
│   ├── IT-Users (Security Group)
│   └── All-Staff (Security Group)
├── HR Departments
│   ├── Emma Wilson (ewilson)
│   ├── David Lee (dlee)
│   └── HR-Users (Security Group)
├── Finance Departments
│   ├── Mike Brown (mbrown)
│   ├── Lisa Chen (lchen)
│   └── Finance-Users (Security Group)
├── Computer Lab
└── Service Accounts
```

---

## 👥 Users Created

| Full Name | Username | Department | Group |
|---|---|---|---|
| John Smith | jsmith | IT | IT-Admin, All-Staff |
| Sarah Jones | sjones | IT | IT-Users, All-Staff |
| Emma Wilson | ewilson | HR | HR-Users, All-Staff |
| David Lee | dlee | HR | HR-Users, All-Staff |
| Mike Brown | mbrown | Finance | Finance-Users, All-Staff |
| Lisa Chen | lchen | Finance | Finance-Users, All-Staff |

---

## 🛡️ Security Groups

| Group Name | Scope | Members |
|---|---|---|
| IT-Admin | Global Security | jsmith |
| IT-Users | Global Security | sjones |
| HR-Users | Global Security | ewilson, dlee |
| Finance-Users | Global Security | mbrown, lchen |
| All-Staff | Global Security | All 6 users |

---

## ⚙️ Group Policy Objects (GPOs)

### 1. Default Domain Policy — Password Policy
Applied to entire domain `sushiit.local`

| Setting | Value |
|---|---|
| Minimum password length | 8 characters |
| Maximum password age | 90 days |
| Minimum password age | 1 day |
| Enforce password history | 5 passwords |
| Password complexity | Enabled |

---

### 2. Default Domain Policy — Screen Lock
Applied to entire domain

| Setting | Value |
|---|---|
| Screen saver timeout | 600 seconds (10 mins) |
| Password protect screen saver | Enabled |

---

### 3. IT-Department-Policy
Applied to IT Departments OU only

| Setting | Value |
|---|---|
| Allow log on locally | IT-Admin group only |

> Only members of IT-Admin can physically log into computers in the IT Department OU. All other users are restricted.

---

### 4. Finance-USB-Block
Applied to Finance Departments OU only

| Setting | Value |
|---|---|
| All Removable Storage classes: Deny all access | Enabled |

> Finance staff cannot use USB drives or any removable storage — enforced for data security compliance.

---

## 💻 PowerShell Commands Used
```powershell
# Apply all GPOs immediately
gpupdate /force

# View all OUs
Get-ADOrganizationalUnit -Filter * | Select-Object Name | Format-Table -AutoSize

# View all users
Get-ADUser -Filter * | Select-Object Name, SamAccountName | Format-Table -AutoSize

# View all groups
Get-ADGroup -Filter * | Select-Object Name | Format-Table -AutoSize

# View all GPOs
Get-GPO -All | Select-Object DisplayName, GpoStatus | Format-Table -AutoSize
```

---

## 📸 Screenshots

| Screenshot | Description |
|---|---|
| `apply_gpo.PNG` | gpupdate /force applied |
| `creating_gpo_for_it_department.PNG` | IT Department GPO |
| `creating_group_and_adding_in_respective_group.PNG` | Security groups and members |
| `department_created.PNG` | OU structure created in AD |
| `finance_usb_policy.PNG` | Finance USB block policy |
| `gpo_edit.PNG` | GPO editor |
| `group_policy.PNG` | Group Policy Management view |
| `info_of_all_the_group_and_user_created_in_different_ous.PNG` | Full AD tree view |
| `set_some_value_in_password_policy.PNG` | Password policy settings |
| `setting_some_policy_for_password.PNG` | Password policy configured |
| `only_it_admin_group_can_access.PNG` | IT login restriction |


---

## 🎯 Skills Demonstrated

- Active Directory Domain Services (AD DS)
- Organisational Unit (OU) design
- User account creation and management
- Security group creation and membership
- Group Policy Object (GPO) creation and linking
- Password policy enforcement
- Screen lock policy deployment
- User rights assignment
- Removable storage restriction
- PowerShell for AD administration

---



---

## 👤 Author
**Sushil Sapkota**
