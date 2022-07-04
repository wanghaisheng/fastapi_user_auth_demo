为了能够自定义页面的组件，让我们直接在amis的编辑器中复制一组演示效果的json ，如下所示



找到你想修改的app对应的admin.py文件，然后找到你对应项修改的某个页面，比如这里我想修改首页进来以后的效果为一组wizard

```
# 注册自定义首页
@site.register_admin
class MyHomeAdmin(admin.HomeAdmin):

    # async def get_page(self, request: Request) -> Page:
    #     # 获取默认页面
    #     page = await super().get_page(request)
    #     # 自定义修改
    #     page.body.title = 'MyHome'
    #     # ...   
    #     return page
    async def get_page(self, request: Request) -> Page:
        page_schema = 'Home Page'
        page = Page.parse_obj(
{
  "type": "page",
  "body": [{
    "type": "panel",
    "title": "我是老手,监控 excel",
    "body": 
    {
      "type": "wizard",
      "title": "准备好了视频文件夹",
      # "api": "/amis/api/mock2/form/saveForm?waitSeconds=2",
      # "initApi": "/amis/api/mock2/form/initData?waitSeconds=2",      
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
              "body":"{excel}",
              "method": 'post'
                },
                        # 解析excel 是否合法有效           
        },

        {
          "title": "从数据库抓取任务，并开始上传",
          "body": [
            "上传视频"
            # 跳转到 定时任务标签下 显示任务正在执行
          ]
        }        
      ]
    }

  },
{
    "type": "panel",
    "title": "我想监控视频文件夹",
    "body": 
    {
      "type": "wizard",
      "title": "准备好了视频文件夹",
      # "api": "/amis/api/mock2/form/saveForm?waitSeconds=2",
      # "initApi": "/amis/api/mock2/form/initData?waitSeconds=2",
      "steps": [
        {
          "title": "选择视频文件夹",
          "body": [
            {
              "name": "videofodler",
              "label": "视频所在文件夹",
              "type": "input-text",


              "required": True
            }
            # ,
            # {
            #   "name": "name",
            #   "label": "名称",
            #   "type": "input-text",
            #   "required": True
            # }
          ]
        },
        {
          "title": "填写配置项",
          "body": [
      {
        "label": "发布频率",
        "type": "select",
        "name": "select",
        "required": True,
        "value": "一次性",

        "options": [
          {
            "label": "定时",
            "value": "cron"
          },
          {
            "label": "间隔",
            "value": "interval"
          },
          {
            "label": "一次性",
            "value": "oneshot"
          }
        ]
      },          
            {
              "name": "start_publish_date",
              "label": "开始公开的日期",
              "value": "+1days",

              "type": "input-date",
              "required": False
            }, 
            {
              "name": "publish_hour_minute",
              "label": "在什么小时公开",
              "value": "10:00",

              "type": "input-time",
              "required": False
            },                       
            {
              "name": "dailycount",
              "label": "每日发布上限",
              "type": "input-number",
              "value": "40",

              "required": True
            },       
            {
              "name": "dailyhourcount",
              "label": "每小时发布上限",
              "type": "input-number",
              "value": "4",

              "required": True
            }
          ]
        },    
        {
          "title": "开始上传",
          "body": [
            "上传视频"
          ]
        }        
      ]
    }



  },]  
}




        )
        return page
```
