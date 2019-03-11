---
title: 大麦后台api文档
date: 2019-03-11 18:08:17
tags: [api文档]
---

#   大麦后台管理系统接口文档

***
### 0. 全局返回结果说明
**接口说明**：全局返回结果   
**全局请求方式**： POST    
**返回格式**：（请求成功）：
```json
{
  "status":true,  //以此为依据判断请求是否成功
  "msg":"",       //请求成功msg无返回值
  "data":[]       // 部分接口返回数组格式数据
}
```
**返回格式**：（请求失败）：
```json
{
  "status":false,    //以此为依据判断请求是否成功
  "msg":"失败原因",   //请求失败原因
  "data":[]          // 请求失败无data返回值
}
```


### 1. 登录
**接口地址**：/home/login/login  
**请求方式**：POST  
**参数校验**：用户名密码不能为空  
**接口描述**：后台管理员登录    
**请求格式**：
```json
{
  "account":"admin",       // 用户名
  "password":"password",   // 密码
  "verify":"verify"        // 验证码，暂时不启用
}

```

### 2.获取订单列表
**接口地址**： /home/index/get_orders    
**参数校验**：无参数    
**接口描述**：获取订单列表   

**成功返回结果**：
```json

{
	"status": true,
	"data": {
		"orders": [{
			"id": "19",                                    // 订单id
			"order_no": "2019030723261672207711311",       // 订单编号
			"no": "001201903074799036",                    // 提货码序列号
			"code": "23286991",                            // 提货码
			"name": "王永喜",                               // 收件人姓名
			"phone": "13776830282",                        // 收件人电话
			"detail": "江苏常州市天宁区城区鼎邦花园25幢1201", // 收件人地址
			"remark": "放门卫",                             // 订单备注
			"num": "2",                                    // 商品数量
			"express_no": "3937303647484",                  // 快递单号
			"express_name": "韵达",                         // 快递名称
			"express_code": "yunda",                        // 快递编码
			"send_time": "2019-03-08 12:36:14",             // 发货时间
			"time": "2019-03-07 23:26:16",                  // 订单创建时间
			"sms_status": "0",                              // 短信发送状态 0未发送1已发送2非导入订单
			"send_status": "1",                             // 发货状态0未发货1已发货
			"goods_info": [{                               // 商品信息数组
				"second_title": "苹果",                       // 二级类目
				"good_remark": "新款",                        // 商品备注
				"first_title": "TPU手机壳",                   // 一级类目
				"good_title": "iphonex"                      // 商品标题
			}, {
				"second_title": "苹果",
				"good_remark": "新款",
				"first_title": "TPU手机壳",
				"good_title": "iphonex"
			}]
		}, {
			"id": "20",
			"order_no": "2019030723261672207711312",
			"no": "001201903074799036",
			"code": "23286991",
			"name": "王永喜",
			"phone": "13776830282",
			"detail": "江苏常州市天宁区城区鼎邦花园25幢1201",
			"remark": "放商店",
			"num": "2",
			"express_no": "3937303647484",
			"express_name": "韵达",
			"express_code": "yunda",
			"send_time": "2019-03-08 12:36:14",
			"time": "2019-03-07 23:26:20",
			"sms_status": "0",
			"send_status": "1",
			"goods_info": [{
				"second_title": "苹果",
				"good_remark": "旧款",
				"first_title": "TPU手机壳",
				"good_title": "iphonex"
			}]
		}, {
			"id": "22",
			"order_no": "2019030723261672207711313",
			"no": "001201903074799036",
			"code": "23286991",
			"name": "王永喜",
			"phone": "13776830282",
			"detail": "江苏常州市天宁区城区鼎邦花园25幢1201",
			"remark": "放商店",
			"num": "2",
			"express_no": "3937303647484",
			"express_name": "韵达",
			"express_code": "yunda",
			"send_time": "2019-03-08 12:36:14",
			"time": "2019-03-07 23:26:20",
			"sms_status": "0",
			"send_status": "1",
			"goods_info": [{
				"second_title": null,
				"good_remark": null,
				"first_title": null,
				"good_title": null
			}]
		}]
	},
	"msg": "请求成功"
}
```
### 3.订单上传（一）
**接口地址**：/home/index/upload_order_first   
**参数校验**：除了remark外所有参数必须非空   
**接口描述**：初始订单上传接口   
**请求格式**:
```json
{
  "platform":"平安好车主",                       // 所属平台
  "name":"张三",                                 // 姓名
  "detail":"江苏常州市天宁区城区鼎邦花园25幢1201", // 详细地址
  "phone":"13323232323",                        // 电话
  "title":"TPU手机壳",                           // 一级类目
  "num":"1",                                    // 数量
  "remark":""                                   // 备注

}
```
### 4.订单上传（二）
**接口地址**：/home/index/upload_order_second  
**参数校验**：所有参数必须非空   
**接口描述**：带物流订单上传接口    
**请求格式**:
```json
{
  "order_no":"2019030723261672207731211", // 订单编号
  "express_name":"顺丰",                  // 快递名称
  "express_no":"3937303647484",           // 快递单号
  "express_code":"shunfeng"               // 快递编码
}
```
### 5.修改订单
**接口地址**：/home/index/update_order  
**参数校验**：所有参数必须非空   
**接口描述**：修改订单接口    
**请求格式**:
```json
{
  "id":"1",                      // 订单id
  "express_id":"2",              // 快递id
  "express_name":"韵达",         // 快递名称
  "express_no":"3937303647484",  // 快递单号
  "express_code":"yunda",        // 快递编号
  "good_id":"1",                 // 商品id
  "remark":"放门卫",             // 商品备注
}
```
### 6.获取类目列表
**接口地址**： /home/index/get_classification   
**参数校验**：无参数  
**接口描述**：获取类目列表   


**成功返回结果**：
```json
{
	"status": true,
	"data": {
		"classification": [{
			"id": "1",                       // 类目id
			"type": "first",                 // 类目种类(一级/二级)
			"title": "TPU手机壳",             // 类目名称
			"pid": null,                     // 所属一级类目(一级类目无此属性)
			"time": "0000-00-00 00:00:00",    // 添加时间
			"status": "1"                    // 状态0禁用1启用
		}, {
			"id": "2",
			"type": "second",
			"title": "iphonex",
			"pid": "1",
			"time": "2019-03-09 13:23:32",
			"status": "1"
		}],
	},
	"msg": "请求成功"
}
```
### 7.添加商品类目
**接口地址**：/home/index/create_good_classification  
**参数校验**：所有参数必须非空   
**接口描述**：添加商品类目接口    
**请求格式**:
```json
{
  "type":"first/second",        // 类目种类（一级类目/二级类目）
  "title":"类目名称",            // 类目名称
  "status":"1",                 // 是否启用（0禁用1启用）
  "pid":"1",                    // 所属一级类目(添加种类为一级类目时此项无效)
}
```

### 8.修改商品类目
**接口地址**：/home/index/update_good_classification  
**参数校验**：所有参数必须非空   
**接口描述**：修改商品类目接口    
**请求格式**:
```json
{
  "id":"1",                     // 类目id
  "title":"类目名称",            // 类目名称
  "status":"1",                 // 是否启用（0禁用1启用）
  "pid":"1",                    // 所属一级类目(修改种类为一级类目时此项无效)
}
```
### 9.获取商品列表
**接口地址**： /home/index/get_goods   
**参数校验**：无参数    
**接口描述**：获取商品列表   

**成功返回数据**：
```json
{
	"status": true,
	"data": {
		"goods": [{
			"id": "1",                               // 商品id
			"second_title": "iphonex",               // 二级类目名称
			"first_title": "TPU手机壳",              // 一级类目名称
			"remark": "新款",                        // 商品备注
			"status": "1",                           // 商品状态0禁用1启用
			"time": "2019-03-09 13:23:49",           // 商品添加时间
			"good_title": "手机保护壳"                // 商品名称
		}],
	},
	"msg": "请求成功"
}
```
### 10.添加商品
**接口地址**：/home/index/create_good  
**参数校验**：所有参数必须非空   
**接口描述**：添加接口    
**请求格式**:
```json
{
  "pid":"2",                   // 二级类目
  "ppid":"1",                  // 一级类目
  "title":"手机保护壳",         // 商品名称
  "remark":"新款",             // 商品备注
  "status":"1",                // 是否启用0禁用1启用
}
```

### 11.修改商品
**接口地址**：/home/index/update_good  
**参数校验**：所有参数必须非空   
**接口描述**：修改商品接口    
**请求格式**:
```json
{
  "id":"1",                    // 商品id
  "pid":"2",                   // 二级类目
  "ppid":"1",                  // 一级类目
  "title":"手机保护壳",         // 商品名称
  "remark":"新款",             // 商品备注
  "status":"1",                // 是否启用0禁用1启用
}
```
### 12.获取类目联动数据
**接口地址**： /home/index/get_sons_info   
**参数校验**：无    
**接口描述**：获取类目联动数据   
**请求格式**:
```json
{
  "type":"first", // 类目种类(一级/二级)
  "id": "1"       // 类目id
}
```

**成功返回数据**：("type = first",返回二级类目数据)
```json
{
	"status": true,
	"data": {
		"info": [{
			"id": "2",         // 类目id
			"title": "iphonex" // 类目名称
		}]
	},
	"msg": "请求成功"
}
```
**成功返回数据**：("type = second",返回商品数据)
```json
{
	"status": true,
	"data": {
		"info": [{
			"id": "1",             // 商品id
			"title": "手机保护壳",  // 商品名称
			"remark": "新款"       // 商品备注
		}]
	},
	"msg": "请求成功"
}
```


### 13.获取提货码列表
**接口地址**：/home/index/get_codes  
**参数校验**：无   
**接口描述**：获取提货码列表接口    

**成功返回数据**：
```json
{
	"status": true,
	"data": {
		"codes": [{
			"id": "1",                               // 提货码id
			"first_title": "TPU手机壳",               // 所属一级类目
			"contacts": "张三",                       // 所属客户
			"status": "1",                           // 提货码状态0作废1启用2暂停
			"stime": "2019-03-07 23:26:16",          // 生成时间
			"etime": "2019-04-06 23:26:16",          // 到期时间
			"no": "001201903074799036",              // 序列号
			"code": "23286991",                      // 提货码
			"link": "http://domain.cn/code/23286991",// 提货链接  
			"use_status": "0"                        // 兑换状态0未兑换1已兑换
		}, {
			"id": "12",
			"first_title": "TPU手机壳",
			"contacts": "张三",
			"status": "1",
			"stime": "2019-03-08 13:38:37",
			"etime": "2019-04-07 13:38:37",
			"no": "001201903086749485",
			"code": "29636468",
			"link": "http://dm.com/code/29636468",
			"use_status": "0"
		}],
	},
	"msg": "请求成功"
}
```
### 14.生成提货码
**接口地址**：/home/index/create_code  
**参数校验**：所有参数必须非空   
**接口描述**：提货码生成接口    
**请求格式**:
```json
{
  "pid":"1",          // 一级类目
  "num":"10",         // 生成数量
  "customer_id":"1",  // 客户id
  "expiry_date":"30", // 有效期（天）
  "status":"1",       // 启用状态（0作废1启用2暂停）
  "use_status":"0"    // 兑换状态（0未兑换1已兑换）
}
```

### 15.修改提货码
**接口地址**：/home/index/update_code  
**参数校验**：所有参数必须非空   
**接口描述**：提货码修改接口    
**请求格式**:
```json
{
  "id":"1",                            // 提货码id
  "pid":"10",                          // 一级类目
  "customer_id":"1",                   // 客户id
  "etime":"2019-03-09 11:11:11",       // 到期日期 YYYY-MM-DD HH:II:SS 格式
  "status":"1"                         // 启用状态（0作废1启用2暂停）
}
```

### 16.信息筛选（待添加）
