# **设置回源Host******

## **1、描述******

设置回源host (setReferHost)

## ****

## **2、请求参数**

**名称******

**类型******

**是否必填******

**描述******username

String

是

京东用户名pinsignature

String

是

用户签名，通过md5的方式校验用户的身份信息，保障信息安全。

md5=日期+username+秘钥SecretKey

日期：格式为 yyyymmdd

username：京东用户名pin

秘钥：双方约定

示例：比如当前日期2016-10-23，用户pin: jcloud_00 ,用户秘钥SecretKey ：e7a31b1c5ea0efa9aa2f29c6559f7d61

那签名为MD5(20161023jcloud_00e7a31b1c5ea0efa9aa2f29c6559f7d61)domain

String

是

加速域名sourceHost

String

是

回源host

## **3、返回参数**

**名称******

**描述******status

结果状态，表示接口请求成功与否，成功用0表示，其他表示失败msg

提示信息，如发送任务失败的原因等data

返回数据

## **4、调用示例**

* 
### **请求地址******

http://opencdn.jcloud.com/api/setReferHost

* 
### **请求示例**

/* json格式
{
“username” :“test_user”,
“signature” :“d00f58f89e8cd55dc080aec0d8051845”,
“domain” :“www.a.com”,
“sourceHost” :“sourcehost1.www.a.com”
}

* 
### **返回示例**

•json格式
{
"status": 0,
"msg": "成功",
"data": "www.a.com"
}