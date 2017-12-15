---
title: Django-ORM-ManyToManyField
date: 2017-12-14 22:34:54
categories:
- Django
- ORM
tags:
---

## 创建models
``` python
class Boy(models.Model):
    username = models.CharField(max_length=16)
    # girls
    def __str__(self):
        return str(self.id)


class Girl(models.Model):
    name = models.CharField(max_length=16)
    boys = models.ManyToManyField('Boy', related_name="girls")
    def __str__(self):
        return str(self.id)
```
## ManyToMany查询
### 正向查询
``` python
# 获取一个女孩对象
g1 = models.Girl.objects.get(id=1)

# 获取和当前女孩有关系的所有男孩
g1.boys.all()                          #获取全部
g1.boys.filter(name='xxx').count() #获取个数
```

### 反向查询
``` python
b1 = models.Boy.objects.get(id=1)
b1.girls.all()                   #获取全部
```

### 连表查询
``` python
## 正向连表
models.Girl.objects.all().values('id','name','boys__username')

## 方向连表
models.Boy.objects.all().values('id','name','girls__name')
```

## ManyToMany添加
``` python
# 正向
g1 = models.Girl.objects.get(id=1)
g1.b.add(models.Boy.objects.get(id=1))
g1.b.add(1)             #可以直接添加ID号

bs = models.Boy.objects.all()
g1.b.add(*bs)               #可以添加列表
g1.b.add(*[1,2,3])      #可以添加ID的列表
```

## ManyToMany 删除
``` python
# 正向
g1 = models.Girl.objects.filter(id=1)

# 删除第三张表中和女孩1关联的所有关联信息
g1.b.clear()        #清空与gilr中id=1 关联的所有数据
g1.b.remove(2)  #可以为id
g1.b.remove(*[1,2,3,4])     #可以为列表,前面加*
```