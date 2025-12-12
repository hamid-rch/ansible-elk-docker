# ELK Ansible Deployment (Full Project)

این پروژه یک دیپلوی کامل ELK Stack روی سروری که حتی هیچ فایل قبلی ندارد ارائه می‌دهد.

## ساختار پروژه
ساختار کامل استاندارد رول Ansible پیاده‌سازی شده است.

## اجرای پروژه
```
ansible-playbook -i inventory/hosts playbooks/site.yml
```

## نکات:
- همه فایل‌ها (docker-compose + config) به صورت خودکار ساخته و کپی می‌شوند
- نیاز به وجود هیچ پوشه یا فایل قبلی روی سرور نیست
