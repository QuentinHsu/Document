# Halo API 文档

**Parameters**：参数

**Responses**：响应

**Response content type**：响应内容类型

## admin-controller

> 管理员控制类接口

### `GET`  /api/admin/counts

Gets count info 获取计数信息

No parameter

```
{
  "attachmentCount": 0,		// 附件数
  "birthday": 0,			    // 生日
  "categoryCount": 0,		  // 种类计数
  "commentCount": 0,		  // 评论计数
  "establishDays": 0,		  // 建立天数
  "journalCount": 0,		  //
  "likeCount": 0,         //
  "linkCount": 0,         // 链接数
  "postCount": 0,         //
  "tagCount": 0,          // 
  "visitCount": 0
}
```

### `GET` /api/admin/environments

Gets environments info 获取环境信息

No parameter

```
{
  "database": "string",     // 数据库
  "mode": "PRODUCTION",     // 模式：生产
  "startTime": 0,           // 开始时间
  "version": "string"       // 版本号
}
```


### `PUT` /api/admin/halo-admin

Updates halo-admin manually 手动更新 halo-admin

No parameter



