---
title: 一个接口适配八个请求
date: 2024-10-17
categories: ["杂谈"]
draft: true
---

肯定有不少人会想：这怎么可能呢？就算用几乎零配置的 SpringBoot，写一个最简单的接口也得有 3 行代码啊！@RequestMapping("test/{request}")
public String test(@PathVariable String request) {
    return request + ": Hello World";
}
那 8 个没啥用的 Hello World 接口就得 24 行代码了！这还没算拼 SQL 连 JDBC 或者调用 ORM 库 的代码呢！更不用说还要写 XML 配置 的其它库了！没错，用传统方式就是这样。获取一个用户：base_url/get/user
获取一个用户列表：base_url/get/user/list
获取一个评论：base_url/get/comment
获取一个评论列表：base_url/get/comment/list
...仅仅是查询，一张表(对应客户端的 model)就要两个接口了，如果再加上增删改，批量改批量删，还有统计，那就得有 8 个接口了！那么我是怎么解决的呢？同一种类型的请求都只用一个接口：增 base_url/post

删（包括批量） base_url/delete

改（包括批量） base_url/put

查（包括列表） base_url/get

统计 base_url/head
用最常用的查询请求举例：获取一个用户：base_url/get/
获取一个用户列表：base_url/get/
获取一个评论：base_url/get
获取一个评论列表：base_url/get
...都是用同一个接口！我是怎么做到的呢？APIJSON，对，就它！我们用 APIJSON 来操作一张表，例如用户表 User，代码写 3 行就够了：//注册表并添加权限，用默认配置
@MethodAccess
public class User {
//内容一般仅供表字段说明及 Android App 开发使用，服务端不用的可不写。
}

//Verifier 内添加权限
accessMap.put(User.class.getSimpleName(), getAccessMap(User.class.getAnnotation(MethodAccess.class)));
或者可以再定制下 POST 请求的角色权限：@MethodAccess(
  POST = {UNKNOWN, ADMIN} //只允许未登录角色和管理员角色新增 User，默认配置是 {LOGIN, ADMIN}
)
public class User {}
然后运行下 Server 工程就可以请求了：URL：http://apijson.cn:8080/get
表单：{
    "User": {
        "id": 82001
    }
}
返回：{
    "User": {
        "id": 82001,
        "sex": 0,
        "name": "Test",
        "tag": "APIJSON User",
        "head": "http://static.oschina.net/uploads/user/19/39085_50.jpg",
        "contactIdList": [
            82004,
            82021,
            70793
        ],
        "pictureList": [
            "http://common.cnblogs.com/images/icon_weibo_24.png"
        ],
        "date": "2017-02-01 19:21:50.0"
    },
    "code": 200,
    "msg": "success"
}
上面只是查了一个 User，如果我们要查女性用户列表，可以这样：URL：http://apijson.cn:8080/get表单：
{
    "[]": { //数组
        "User": {
            "sex": 1, //性别为女
            "@column": "id,name" //只需要id,name这两个字段
        }
    }
}
返回：{
    "[]": [
        {
            "User": {
                "id": 82002,
                "name": "Happy~"
            }
        },
        {
            "User": {
                "id": 82003,
                "name": "Wechat"
            }
        },
        {
            "User": {
                "id": 82005,
                "name": "Jan"
            }
        }
    ],
    "code": 200,
    "msg": "success"
}
User 被多包裹了一层？给数组命名为 User[] 来去掉吧：表单：{
    "User[]": { //提取User
        "User": {
            "sex": 1, //性别为女
            "@column": "id,name" //只需要id,name这两个字段
        }
    }
返回：{
    "User[]": [
        {
            "id": 82002,
            "name": "Happy~"
        },
        {
            "id": 82003,
            "name": "Wechat"
        },
        {
            "id": 82005,
            "name": "Jan"
        }
    ],
    "code": 200,
    "msg": "success"
}
还要进一步提取名字？User-name[] 满足你：表单：{
    "User-name[]": { //提取User.name
        "User": {
            "sex": 1, //性别为女
            "@column": "name" //只需要name这个字段
        }
    }
}
返回：{
    "User-name[]": [
        "Happy~",
        "Wechat",
        "Jan",
        "Meria",
        "Tommy"
    ],
    "code": 200,
    "msg": "success"
}
但如果是含多张表关联的数组，就不要去掉了哦：表单：{
    "[]": {
        "Comment": {}, //评论
        "User": {      //发布评论的用户
            "id@": "/Comment/userId" //User.id = Comment.userId
        }
    }
}
返回：{
    "[]": [
        {
            "Comment": {
                "id": 3,
                "toId": 0,
                "userId": 82002,
                "momentId": 15,
                "date": "2017-02-01 19:20:50.0",
                "content": "This is a Content...-3"
            },
            "User": {
                "id": 82002,
                "sex": 1,
                "name": "Happy~",
                "tag": "iOS",
                "head": "http://static.oschina.net/uploads/user/1174/2348263_50.png?t=1439773471000",
                "contactIdList": [
                    82005,
                    82001,
                    38710
                ],
                "pictureList": [],
                "date": "2017-02-01 19:21:50.0"
            }
        },
        {
            "Comment": {
                "id": 4,
                "toId": 0,
                "userId": 38710,
                "momentId": 470,
                "date": "2017-02-01 19:20:50.0",
                "content": "This is a Content...-4"
            },
            "User": {
                "id": 38710,
                "sex": 0,
                "name": "TommyLemon",
                "tag": "Android&Java",
                "head": "http://static.oschina.net/uploads/user/1218/2437072_100.jpg?t=1461076033000",
                "contactIdList": [
                    82003,
                    82005
                ],
                "pictureList": [
                    "http://static.oschina.net/uploads/user/1218/2437072_100.jpg?t=1461076033000",
                    "http://common.cnblogs.com/images/icon_weibo_24.png"
                ],
                "date": "2017-02-01 19:21:50.0"
            }
        }
    ],
    "code": 200,
    "msg": "success"
}
还有动态 Moment 和它的点赞用户列表：{
    "Moment": {},
    "User[]": {
        "User": {
            "id{}@": "Moment/praiseUserIdList" //id在点赞列表praiseUserIdList内
        }
    }
}
类似微信个人资料界面：{
    "User": {},
    "Moment[]": { //朋友圈照片列表
        "Moment": {
            "@order":"date-", //按发布时间date倒序排列
            "userId@": "User/id"
        }
    }
}
类似微信朋友圈的动态列表：{
    "[]": {
        "count": 3, //只要3个
        "page": 2,  //要第2页的
        "Moment": {},
        "User": {
            "id@": "/Moment/userId"
        },
        "Comment[]": {
            "Comment": {
                "momentId@": "[]/Moment/id"
            }
        }
    }
}
...任意结构，任意内容，任意组合，想要什么 JSON 结构、字段内容、表关联组合查询都可以完全自定义！"key[]":{}                                         // 查询数组

"key{}":[1,2,3]                                    // 匹配选项范围

"key{}":"<=10,length(key)>1..."                    // 匹配条件范围

"key()":"function(arg0,arg1...)"                   // 远程调用函数

"key@":"key0/key1.../targetKey"                    // 引用赋值

"key$":"%abc%"                                     // 模糊搜索

"key?":"^[0-9]+$"                                  // 正则匹配

"key+":[1]                                         // 增加/扩展

"key-":888.88                                     // 减少/去除

"name:alias"                                      // 新建别名

"@column":"id,sex,name"                           // 返回字段

"@group":"userId"                                 // 分组方式

"@having":"max(id)>=100"                          // 聚合函数

"@order":"date-,name+"                            // 排序方式

以上都是查询请求，再试试 增删改 和 统计 ：增: http://apijson.cn:8080/post{
    "Comment": {
        "userId": 82001,
        "momentId": 15,
        "content": "测试新增评论"
    },
    "tag": "Comment"
}
删: http://apijson.cn:8080/delete{
    "Comment": {
        "id": 1510394480987
    },
    "tag": "Comment"
}
改: http://apijson.cn:8080/put{
    "Comment": {
        "id": 22,
        "content": "测试修改评论"
    },
    "tag": "Comment"
}
批量删: http://apijson.cn:8080/delete{
    "Comment": {
        "id{}": [1510394480987, 1510394804925]
    },
    "tag": "Comment[]"
}
批量改: http://apijson.cn:8080/put{
    "Comment": {
        "id{}": [22, 114],
        "content": "测试批量修改评论"
    },
    "tag": "Comment[]"
}
统计: http://apijson.cn:8080/head{
    "Comment": {
        "content$": "%测试%" //内容包含 测试 两个字
    }
}
写操作需要对应的权限，就是用 3 行代码配置的，请求报错：登录后角色自动变为 LOGIN(可传@role 来自定义)，符合 Comment 的 POST 权限配置，成功：回想下，代码才写了 3 行，就实现了包括增删改查等各种操作的 8 个接口以及这么多种查询！事实上用 APIJSON 根本就不用自己写接口！这 3 行代码其实是为了做权限管理！像个人博客、非商业的新闻资讯网站这种可以没有权限控制的，改下全局配置，不做权限校验，那就连一行代码都不用写了！！！