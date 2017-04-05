# ISC+ 后台系统接口文档

> 接口中的“优先级”按 1 > 2 > 3 > 4 确定，1 最大，4最小，其中 3、4 级别的接口可以在下期（2017.7.1-）工作中完善。

## 1. 卡片增量接口

- 用途：dashboard 页展示卡片增量，返回 N 天内上传的卡片数量
- 优先级：2
- path: 
- method: GET
- query params: 

```
day=7 // 表示请求 7 天的增量数
```

- response: 

```javascript
{
  code: 0,
  success: true,
  data: {
    count: 28  // 增量值
  }
}
```

## 2. 卡片引用排行榜

- 用途：dashboard 页展示卡片引用排行榜
- 优先级：3
- path: 
- method: GET
- query params: 

```javascript
limit=5 // 表示接口返回被引用最高的前 5 个卡片
```

- response: 

```javascript
{
  code: 0,
  success: true,
  data: {
    rank: [ // rank 数组中的值按 top 1,2,3,4,5 依次排列
      {
        name: '卡片名称',
        count: 291 // 被引用的数量
      }, {...}, {...}, {...}, {...}
    ]
  }
}
```

## 3. 我的卡片列表

- 用途：我的卡片页展示卡片列表，返回按修改时间排序的数据
- 优先级：1
- path: 
- method: GET
- query params: 

```javascript
page=1 // 表示当前页面序号
count=10 // 表示每页返回 10 条数据
```

- response: 

```javascript
{
  code: 0,
  success: true,
  data: {
    list: [
      {
        name: '卡片名称',
        id: 1,
        author: 'ISC+',
        updateTime: '2017.4.1',
        type: 1, // type 状态码对应卡片类型
        category: 1, // category 状态码对应卡片分类
        status: 1 // status 状态码对应卡片状态
      }, {...}, {...}, {...}, {...}, {...}, {...}, {...}, {...}, {...}
    ]
  }
}
```

## 4. 卡片上架请求

- 用途：用户点击上架按钮后可将“已下架”卡片重新上架

> 卡片未审核状态用户无法上架卡片，只有审核通过后，用户通过点击下架按钮，卡片下架后，才可能出现上架请求。

- 优先级：1
- path: 
- method: POST
- query params: -
- post data:

```javascript
user: 'c00385832',
id: 1 // 卡片 ID
```

- response: 

```javascript
{
  code: 0,
  success: true
}
```

## 5. 卡片下架请求

- 用途：用户点击下架按钮后可将“已上架”卡片下架

- 优先级：1
- path: 
- method: POST
- query params: -
- post data:

```javascript
user: 'c00385832',
id: 1 // 卡片 ID
```

- response: 

```javascript
{
  code: 0,
  success: true
}
```

## 6. 卡片删除请求

- 用途：用户点击删除按钮后可将“已下架”、“驳回” 的卡片删除

- 优先级：1
- path: 
- method: POST
- query params: -
- post data:

```javascript
user: 'c00385832',
id: 1 // 卡片 ID
```

- response: 

```javascript
{
  code: 0,
  success: true
}
```

## 7. 卡片预览请求

- 用途：用户点击预览按钮后可预览卡片，服务端返回卡片相关内容

- 优先级：1
- path: 
- method: GET
- query params: 

```javascript
user: 'c00385832',
id: 1 // 卡片 ID
```

- response: 

```javascript
{
  code: 0,
  success: true,
  data: {
    card: {
      ... // 卡片数据模型
    }
  }
}
```

## 8. 批准卡片请求

- 用途：超级 Admin 点击批准按钮后卡片从审核状态变更为上架状态

- 优先级：1
- path: 
- method: POST
- query params: -
- post data:

```javascript
user: 'c00385832',
id: 1 // 卡片 ID
```

- response: 

```javascript
{
  code: 0,
  success: true
}
```

## 9. 驳回卡片请求

- 用途：超级 Admin 点击驳回按钮后卡片从审核状态变更为驳回状态

- 优先级：1
- path: 
- method: POST
- query params: -
- post data:
```javascript
user: 'c00385832',
id: 1 // 卡片 ID
```

- response: 

```javascript
{
  code: 0,
  success: true
}
```


## 10. 审核卡片列表

- 用途：审核卡片页面列表数据展示，按卡片的提交审核时间排序

- 优先级：1
- path: 
- method: GET
- query params: 

```javascript
page=1 // 表示当前页面序号
count=10 // 表示每页返回 10 条数据
```

- response: 

```javascript
{
  code: 0,
  success: true,
  data: {
    list: [
      {
        name: '卡片名称',
        id: 1,
        author: 'ISC+',
        updateTime: '2017.4.1',
        type: 1, // type 状态码对应卡片类型
        category: 1, // category 状态码对应卡片分类
        status: 1 // status 状态码对应卡片状态
      }, {...}, {...}, {...}, {...}, {...}, {...}, {...}, {...}, {...}
    ]
  }
}
```

## 11. 卡片名称检查请求

- 用途：用户新建卡片时，需要检查卡片名称是否被占用

- 优先级：1
- path: 
- method: POST
- query params: -
- post data:

```javascript
name: '卡片名称'
```

- response: 

```javascript
{
  code: 0,
  success: true,
  data: {
    result: true 
  }
}
```

## 12. 新建卡片请求

- 用途：用户提交新建卡片表单

- 优先级：1
- path: 
- method: POST
- query params: -
- post data:
```javascript
user: 'c00385832'
name: '卡片名称'
type: 1
category: 1
width: 1
height: 1
role: '角色1,角色2,角色3'
data: '{...}' // 卡片的 JSON 数据,
desc: '卡片描述信息'
```

- response: 

```javascript
{
  code: 0,
  success: true,
  data: {
    card: {...} //卡片数据模型
  }
}
```

## 13. 修改卡片请求

- 用途：用户提交修改卡片表单

- 优先级：1
- path: 
- method: POST
- query params: -
- post data:
```javascript
user: 'c00385832'
id: 1
name: '卡片名称'
type: 1
category: 1
width: 1
height: 1
role: '角色1,角色2,角色3'
data: '{...}' // 卡片的 JSON 数据,
desc: '卡片描述信息'
```

- response: 

```javascript
{
  code: 0,
  success: true,
  data: {
    card: {...} //卡片数据模型
  }
}
```

-------------

-------------

-------------

## 数据接口返回规则：

### success

```javascript
{
  code: 0,
  success: true,
  data: {...} // data 字段存放需要返回的信息，无必须信息时可省略
}
```

### error

```javascript
{
  code: -1,
  success: false,
  message: "错误信息提示语句"
}
```

-------------

-------------

-------------

## type 状态码

type 状态码对应卡片的类型

- 1 - 自定义
- 2 - 表格
- 3 - 折线图
- 4 - 环形图
- 5 - 柱状图

## category 状态码

category 状态码对应卡片的分类

- 1 - 通用

## status 状态码

status 状态码对应卡片的状态

- 1 - 
- 2 - 
- 3 - 

-------------

-------------

-------------
