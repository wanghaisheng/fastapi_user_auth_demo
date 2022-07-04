示例跑起来以后，你想按照自己的思路增加一个左侧的菜单，然后在不影响demo主体的情况下进行玩耍


1. 打开fastapi_user_auth_demo\backend\main.py ，假如这里我复制了整个blog文件夹，并重命名为publish，那么在该文件中我需要添加如下两行，当然，为了数据库中表名不冲突的情况下，你在复制了文件夹以后需要修改models.py里面相应的名称

```
# 安装应用 publish
from apps import publish

publish.setup(app)
```

2.如果正常的话 你可以刷新浏览器界面看到效果
