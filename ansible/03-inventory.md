# Ansible - الـ Inventory

## إيه هو الـ Inventory؟

الـ **Inventory** ده ملف بتحدد فيه كل السيرفرات (الـ hosts) اللي عايز Ansible يشتغل عليها.

ممكن يكون بصيغة **INI** أو **YAML**.

---

## Inventory بصيغة INI

### مثال بسيط:
```ini
[webservers]
web1.example.com
web2.example.com
192.168.1.10

[databases]
db1.example.com
db2.example.com
```

### مع بيانات إضافية:
```ini
[webservers]
web1.example.com ansible_user=ubuntu ansible_port=2222
web2.example.com ansible_user=admin

[databases]
db1.example.com ansible_host=192.168.1.20 ansible_user=root
```

---

## Inventory بصيغة YAML

```yaml
all:
  children:
    webservers:
      hosts:
        web1.example.com:
        web2.example.com:
    databases:
      hosts:
        db1.example.com:
          ansible_host: 192.168.1.20
          ansible_user: root
```

---

## الـ Variables في Inventory

### Host Variables (خاصة بـ host واحد):
```ini
[webservers]
web1.example.com http_port=80 max_connections=500
```

### Group Variables (خاصة بمجموعة):
```ini
[webservers:vars]
ansible_user=ubuntu
ansible_python_interpreter=/usr/bin/python3
```

---

## استخدام الـ Inventory

```bash
# استخدام ملف inventory محدد
ansible all -i inventory.ini -m ping

# استخدام group معين
ansible webservers -i inventory.ini -m ping

# استخدام host واحد
ansible web1.example.com -i inventory.ini -m ping
```

---

## Dynamic Inventory (متقدم)

لما يكون عندك سيرفرات كتير على AWS أو Azure، ممكن تستخدم **Dynamic Inventory** بدل ما تكتبهم يدوي.

```bash
# مثال مع AWS
ansible-inventory -i aws_ec2.yml --graph
```

---

## خلاصة الدرس 📌

- الـ Inventory = قائمة بالسيرفرات
- ممكن يكون INI أو YAML
- نقدر نحدد variables لكل host أو group
- في Dynamic Inventory للبيئات الكبيرة
