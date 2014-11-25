Magic Stone API
================

#### 客户端权限验证

  - header填充api id及api key

  - X-AVOSCloud-Application-Id = f5m9v06xzyjdah7075xp3xo47l8gxmah5l9nqsvn12ewk87n

  - X-AVOSCloud-Application-Key = zo3d1f2kz5chpujm6rtqetk9lls115k2exvhbbuzap62secs



#### 登录api

  - URL: https://leancloud.cn/1.1/login?username=liuyuxiao123&password=19900410lyx

  - api参数说明：参数包含在请求的url中 
               username=liuyuxiao123
               password=19900410lyx

  - 支持格式：json
    
  - HTTP请求方式: GET 
           
  - 返回数据：

    {
      "username": "cooldude6",
      "sessionToken": "hrphjmsubxm56za56pxc6m3jr",
      "mobilePhoneVerified": false,
      "phone": "415-392-0202",
      "createdAt": "2014-11-24T10:17:26.676Z",
      "objectId": "547305b6e4b0ed4838dcf878",
      "emailVerified": false,
      "updatedAt": "2014-11-24T10:17:26.676Z"
    }




#### 获取指定用户project列表api


  - URL: https://leancloud.cn/1.1/classes/Project?limit=10&order=-updatedAt&skip=0&where={"userName":"duzhangtech"}

  - api参数说明：参数包含在请求的url中 
               limit=10 数量上限
               skip=0 起始位置
               order=-updatedAt 按修改时间排序
               where={"userName":"duzhangtech"} 查询用户帐号

  - 支持格式：json
    
  - HTTP请求方式: GET 

  - 返回数据：

   {
    "results": [
        {
            "status": "等待客服确认",
            "leads": 0,
            "projectName": "created by duzhang 2",
            "budget": 0,
            "projectStartTime": {
                "iso": "2014-11-25T04:49:11.000Z",
                "__type": "Date"
            },
            "impressions": 0,
            "clicks": 0,
            "projectEndTime": {
                "iso": "2014-11-29T05:01:22.000Z",
                "__type": "Date"
            },
            "createdAt": "2014-11-25T04:48:57.532Z",
            "objectId": "54740a39e4b0ed4838e1b670",
            "userName": "duzhangtech",
            "cost": 0,
            "updatedAt": "2014-11-25T05:01:31.870Z"
        },
        {
            "status": "等待客服确认",
            "leads": 0,
            "projectName": "created by duzhang",
            "budget": 0,
            "projectStartTime": {
                "iso": "2014-11-25T04:46:20.000Z",
                "__type": "Date"
            },
            "impressions": 0,
            "clicks": 0,
            "projectEndTime": {
                "iso": "2014-12-25T04:46:52.000Z",
                "__type": "Date"
            },
            "createdAt": "2014-11-25T04:43:53.953Z",
            "objectId": "54740909e4b0ed4838e1ad5d",
            "userName": "duzhangtech",
            "cost": 0,
            "updatedAt": "2014-11-25T04:47:01.248Z"
        }
    ]
}

  
 


