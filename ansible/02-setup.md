# Ansible - التنصيب والإعداد (Setup)

## متطلبات التنصيب

### على الـ Control Node (جهازك):
- Python 3.8 أو أحدث
- Linux أو macOS (Windows ممكن بس عن طريق WSL)

### على الـ Managed Nodes (السيرفرات):
- Python 3
- SSH متاح
- User عنده sudo permissions

---

## تنصيب Ansible

### على Ubuntu/Debian:
```bash
sudo apt update
sudo apt install software-properties-common
sudo add-apt-repository --yes --update ppa:ansible/ansible
sudo apt install ansible
```

### على CentOS/RHEL:
```bash
sudo yum install epel-release
sudo yum install ansible
```

### باستخدام pip (أي نظام):
```bash
pip3 install ansible
```

### تأكد من التنصيب:
```bash
ansible --version
```

---

## إعداد SSH للاتصال بالسيرفرات

### 1. توليد SSH Key:
```bash
ssh-keygen -t rsa -b 4096
```

### 2. نسخ الـ Public Key للسيرفرات:
```bash
ssh-copy-id user@192.168.1.10
ssh-copy-id user@192.168.1.11
```

### 3. تجربة الاتصال:
```bash
ssh user@192.168.1.10
```

---

## إنشاء أول Inventory File

إنشئ ملف اسمه `hosts`:

```ini
[webservers]
192.168.1.10
192.168.1.11

[databases]
192.168.1.20
```

---

## أول اختبار

جرّب الأمر ده عشان تتأكد إن كل حاجة شغالة:

```bash
ansible all -i hosts -m ping
```

لو شفت رسالة `"pong"` يبقى كله تمام! ✅

---

## خلاصة الدرس 📌

- نصّبنا Ansible على الـ Control Node
- عملنا SSH keys عشان نتصل بالسيرفرات بدون password
- عملنا أول inventory file
- جرّبنا أول أمر ansible (ping)
