demo中自带的例子 跑起来以后会有新增和批量新增两个按钮，批量新增允许你导入一个已有的excel实现数据的批量入库，这里我定义了一个wizard，第一步里留了excel导入的组件，现在想通过点击下一步，
完成数据的入库

```
      "steps": [
        {
          "title": "选择excel文件 保存数据到数据库",
          "body": [
            {
              "name": "excelpath",
              "label": "excel路径",
              "type": "input-excel",
              "required": True
            }
            # ,
            # {
            #   "name": "name",
            #   "label": "名称",
            #   "type": "input-text",
            #   "required": True
            # }
          ],
          "api": {
              "url":"/admin/publish/videoadmin/item",     
              "body":"${excel}",
              "method": 'post'
                },
                        # 解析excel 是否合法有效           
        },
```

当我用官方的https://aisuda.bce.baidu.com/amis/zh-CN/components/form/input-excel来试验我准备的excel
上传以后的数据是什么样的时候，
```
{
  "excel": [
    {
      "id": 1,
      "title": "video-test-01",
      "prefertitlehashtag": "",
      "img": "/admin/upload/202206\\f07a86b0752f4f868a15570ab99287f4.png",
      "horizon_thumb": "",
      "vertical_thumb": "",
      "description_prefix": "前缀",
      "description_middle": "正文",
      "prefertags": "标签1,标签2,标签3",
      "description_suffix": "后缀",
      "tags": "标签6,标签5,标签4",
      "description": "",
      "status": 0,
      "publishpolicy": 1,
      "update_time": "2022-06-30T02:54:01.509234",
      "schedule_time": "2022-07-01T00:00:00",
      "publish_hour_minute": "",
      "local_path": "",
      "fileURL": "",
      "username": "",
      "password": "",
      "recovery_email": "",
      "proxy_ip": "",
      "cookie_path": "",
      "backupchannel": 4,
      "channel_id": 4,
      "platform_id": "",
      "user_id": 1
    },
    {
      "id": 2,
      "title": "video-test-01",
      "prefertitlehashtag": "",
      "img": "/admin/upload/202206\\f07a86b0752f4f868a15570ab99287f4.png",
      "horizon_thumb": "",
      "vertical_thumb": "",
      "description_prefix": "前缀",
      "description_middle": "正文",
      "prefertags": "标签1,标签2,标签3",
      "description_suffix": "后缀",
      "tags": "标签6,标签5,标签4",
      "description": "",
      "status": 0,
      "publishpolicy": 1,
      "update_time": "2022-06-30T02:54:01.509234",
      "schedule_time": "2022-07-01T00:00:00",
      "publish_hour_minute": "",
      "local_path": "",
      "fileURL": "",
      "username": "",
      "password": "",
      "recovery_email": "",
      "proxy_ip": "",
      "cookie_path": "",
      "backupchannel": 4,
      "channel_id": 4,
      "platform_id": "",
      "user_id": 1
    },
    {
      "id": 3,
      "title": "video-test-01",
      "prefertitlehashtag": "",
      "img": "/admin/upload/202206\\f07a86b0752f4f868a15570ab99287f4.png",
      "horizon_thumb": "",
      "vertical_thumb": "",
      "description_prefix": "前缀",
      "description_middle": "正文",
      "prefertags": "标签1,标签2,标签3",
      "description_suffix": "后缀",
      "tags": "标签6,标签5,标签4",
      "description": "",
      "status": 0,
      "publishpolicy": 1,
      "update_time": "2022-06-30T02:54:01.509234",
      "schedule_time": "2022-07-01T00:00:00",
      "publish_hour_minute": "",
      "local_path": "",
      "fileURL": "",
      "username": "",
      "password": "",
      "recovery_email": "",
      "proxy_ip": "",
      "cookie_path": "",
      "backupchannel": 4,
      "channel_id": 4,
      "platform_id": "",
      "user_id": 1
    },
    {
      "id": 4,
      "title": "video-test-01",
      "prefertitlehashtag": "",
      "img": "/admin/upload/202206\\f07a86b0752f4f868a15570ab99287f4.png",
      "horizon_thumb": "",
      "vertical_thumb": "",
      "description_prefix": "前缀",
      "description_middle": "正文",
      "prefertags": "标签1,标签2,标签3",
      "description_suffix": "后缀",
      "tags": "标签6,标签5,标签4",
      "description": "",
      "status": 0,
      "publishpolicy": 1,
      "update_time": "2022-06-30T02:54:01.509234",
      "schedule_time": "2022-07-01T00:00:00",
      "publish_hour_minute": "",
      "local_path": "",
      "fileURL": "",
      "username": "",
      "password": "",
      "recovery_email": "",
      "proxy_ip": "",
      "cookie_path": "",
      "backupchannel": 4,
      "channel_id": 4,
      "platform_id": "",
      "user_id": 1
    }
  ]
}```

我发现excel解析后是这么个结构,所以我在上面的amis json里新加了一个body字段，希望能通过${excel}来拿到数组，但跑起来发现数组还是被包在一个奇怪的excelpath下面，我就有点束手无策
![image](https://user-images.githubusercontent.com/2363295/177198668-f29db488-6bef-47bb-a9af-1b69795aa748.png)

