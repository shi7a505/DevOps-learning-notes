# 🧠 Ad Hoc Commands in Ansible

الـ **Ad Hoc Commands** هي طريقة سريعة لتنفيذ أوامر مؤقتة على السيرفرات من غير ما تكتب Playbook كامل.  
بتستخدمها لما تكون عايز تعمل حاجة بسيطة زي اختبار الاتصال، أو تشغيل خدمة، أو تحديث باكدج.

---

## 🧩 البنية الأساسية للأمر

```bash
ansible <hosts> -i <inventory_file> -m <module_name> -a "<arguments>"
```

### شرح الأجزاء:

- `<hosts>` → ممكن تكون `all` أو group معين زي `webservers`.
- `-i` → تحدد ملف الـ inventory اللي فيه السيرفرات.
- `-m` → الموديول اللي هتستخدمه.
- `-a` → البراميترز أو الأوامر اللي هتتبعت للموديول.

---

## 🔹 أمثلة عملية

### ✅ اختبار الاتصال بالسيرفرات

```bash
ansible all -i inventory.ini -m ping
```

ده بيتأكد إن كل السيرفرات شغالة وإن Ansible شايفها تمام.

---

### 💻 تشغيل أمر Shell على السيرفرات

```bash
ansible webservers -i inventory.ini -m shell -a "uptime"
```

بيشغّل أمر `uptime` على كل السيرفرات اللي في الـ group اسمه `webservers`.

---

### 📁 نسخ ملف من الجهاز المحلي للسيرفر

```bash
ansible all -i inventory.ini -m copy -a "src=/home/user/test.txt dest=/tmp/"
```

---

### 📦 تثبيت Package على السيرفرات (مثلاً nginx)

```bash
ansible all -i inventory.ini -m yum -a "name=nginx state=present"
```

> لو السيرفرات Ubuntu استخدم `apt` بدل `yum`.

---

### 🔧 تشغيل أو إيقاف خدمة

```bash
ansible all -i inventory.ini -m service -a "name=nginx state=started"
```

---

### 🗑️ حذف Package

```bash
ansible all -i inventory.ini -m yum -a "name=nginx state=absent"
```

---

## 💡 ملاحظات مهمة

- **استخدم `-b` لو محتاج صلاحيات sudo:**

```bash
ansible all -i inventory.ini -b -m yum -a "name=nginx state=present"
```

- **استخدم `--limit` لتحديد سيرفر معين:**

```bash
ansible all -i inventory.ini -m ping --limit web01
```

---

## 🎯 الخلاصة

الـ **Ad Hoc Commands** مفيدة جدًا لو عايز تنفذ أوامر سريعة بدون ما تجهز Playbook كامل،  
لكن لو هتكرر نفس العمليات أو محتاج Tasks متربطة، ساعتها الـ **Playbook** هو الحل الأفضل.
