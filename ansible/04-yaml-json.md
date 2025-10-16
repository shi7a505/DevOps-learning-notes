# YAML و JSON - الأساسيات

## ليه محتاجين نفهم YAML؟

لأن **كل الـ Playbooks في Ansible بتتكتب بـ YAML!**

YAML = YAML Ain't Markup Language (لغة بسيطة لتنظيم البيانات)

---

## الفرق بين YAML و JSON

### نفس البيانات بـ JSON:
```json
{
  "name": "Ahmed",
  "age": 25,
  "skills": ["Python", "Ansible", "AWS"],
  "address": {
    "city": "Cairo",
    "country": "Egypt"
  }
}
```

### نفس البيانات بـ YAML:
```yaml
name: Ahmed
age: 25
skills:
  - Python
  - Ansible
  - AWS
address:
  city: Cairo
  country: Egypt
```

شايف الفرق؟ YAML أبسط وأسهل في القراءة! 😎

---

## قواعد كتابة YAML

### 1. الـ Indentation (المسافات) مهمة جداً!
```yaml
# ✅ صح
parent:
  child: value

# ❌ غلط
parent:
 child: value
```

### 2. القوائم (Lists):
```yaml
fruits:
  - Apple
  - Orange
  - Banana
```

### 3. الـ Dictionaries (Key-Value):
```yaml
person:
  name: Mohamed
  age: 30
  job: DevOps Engineer
```

### 4. القوائم من Dictionaries:
```yaml
users:
  - name: Ahmed
    age: 25
  - name: Sara
    age: 28
```

---

## أمثلة عملية في Ansible

### Playbook بسيط:
```yaml
---
- name: Install packages
  hosts: webservers
  tasks:
    - name: Install nginx
      apt:
        name: nginx
        state: present
```

### Playbook فيه أكتر من task:
```yaml
---
- name: Setup web server
  hosts: webservers
  tasks:
    - name: Install nginx
      apt:
        name: nginx
        state: present
    
    - name: Start nginx
      service:
        name: nginx
        state: started
```

---

## نصائح عشان متتلخبطش في YAML

✅ استخدم spaces (مش tabs!)  
✅ كل level جديد = مسافتين  
✅ اتأكد من الـ syntax بأداة زي [yamllint](http://www.yamllint.com/)

---

## خلاصة الدرس 📌

- YAML أسهل من JSON
- الـ indentation مهم جداً
- كل playbook في Ansible بيبدأ بـ `---`
- نستخدم lists (`-`) و dictionaries (`key: value`)
