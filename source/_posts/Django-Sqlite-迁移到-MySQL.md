---
title: Django Sqlite 迁移到 MySQL
date: 2020-04-15 11:44:49
tags: Python
---

Sqlite在前期测试，开发提供的极大的便捷性。本文解决从Django的默认数据库（Sqlite）迁移数据到MySQL。

#### 第一步：`Django Settings` 配置数据库
<!--more-->
```
DATABASES = {
    ‘default’: {
        ‘ENGINE’: ‘django.db.backends.sqlite3’,
        ’NAME’: os.path.join(BASE_DIR, ‘db.sqlite3’),
    },

    ’slave’: {
        ‘ENGINE’: ‘django.db.backends.mysql’,
        ’NAME’: ‘welfare’,
        ‘USER’: ‘welfare’,
        ‘PASSWORD’: *****,
        ‘HOST’: ‘192.168.XXX.XXX’,
        ‘PORTT’: ‘3306’,
    }
}
```


#### 第二步：将`migrations`记录同步到`slave`数据库
**mysql中新建welfare库**
```sql
CREATE DATABASE welfare CHARACTER SET utf8 COLLATE utf8_general_ci;
```
**用户授权**
```sql
grant all privileges on welfare.* to "welfare”@“%" identified by “Root123.”;
```
**同步migrate操作**
```sql
python manage.py migrate --database slave
```

#### 第三步：导出`sqlite3`数据
```bash
python manage.py dumpdata --database default > datadump20190917.json
```

#### 第四步：导入数据
```bash
python manage.py loaddata --database slave < datadump20190917.json
```

**错图提示**
> django.db.utils.IntegrityError: Problem installing fixture '/Users/yanghao/PycharmProjects/welfare/datadump20190917.json': Could not load contenttypes.ContentType(pk=12): (1062, "Duplicate entry 'django_apscheduler-djangojob' for key 'django_content_type_app_label_model_76bd3d3b_uniq'")
>
**解决方式**
因为 auth_permission， django_content_type中存在数据，这些数据是migrate时产生的content_type相关表
```
   delete from auth_permission;
   delete from django_content_type;
```

#### 第五步：修改Mysql为默认数据库
```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': db_name,
        'USER': db_user,
        'PASSWORD': db_pwd,
        'HOST': db_host,
    }
}
```
