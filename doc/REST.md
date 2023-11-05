# RESTful api

## 风格

- GET（SELECT）：从服务器取出资源（一项或多项）。
- POST（CREATE）：在服务器新建一个资源。
- PUT（UPDATE）：在服务器更新资源（客户端提供完整资源数据）。
- PATCH（UPDATE）：在服务器更新资源（客户端提供需要修改的资源数据）。
- DELETE（DELETE）：从服务器删除资源。

## 设计规范

URL组成：
`URI = scheme "://" host  ":"  port "/" path [ "?" query ][ "#" fragment ]`

RESTful API组成:
`/{version}/{resources}/{resource_id}`

version：API版本号，有些版本号放置在头信息中也可以，通过控制版本号有利于应用迭代。
resources：资源，RESTful API推荐用小写英文单词的复数形式。
resource_id：资源的id，访问或操作该资源。

可细分很多子资源
`/{version}/{resources}/{resource_id}/{subresources}/{subresource_id}`

有时可能增删改查无法满足业务要求，可以在URL末尾加上action
`/{version}/{resources}/{resource_id}/action`

规范：

1. 不用大写字母，所有单词使用英文且小写。
2. 连字符用中杠"-"而不用下杠"_"
3. 正确使用 "/"表示层级关系,URL的层级不要过深，并且越靠前的层级应该相对越稳定
4. 结尾不要包含正斜杠分隔符"/"
5. URL中不出现动词，用请求方式表示动作
6. 资源表示用复数不要用单数
7. 不要使用文件扩展名

在非rest风格中请求url通常以动词出现
而rest风格中请求以名称出现，操作从请求方式中看出来

## 状态码

> 1xx：相关信息
> 2xx：操作成功
> 3xx：重定向
> 4xx：客户端错误
> 5xx：服务器错误

200 OK - [GET]：服务器成功返回用户请求的数据，该操作是幂等的（Idempotent）。
201 CREATED - [POST/PUT/PATCH]：用户新建或修改数据成功。
202 Accepted - [*]：表示一个请求已经进入后台排队（异步任务）
204 NO CONTENT - [DELETE]：用户删除数据成功。
400 INVALID REQUEST - [POST/PUT/PATCH]：用户发出的请求有错误，服务器没有进行新建或修改数据的操作，该操作是幂等的。
401 Unauthorized - [*]：表示用户没有权限（令牌、用户名、密码错误）。
403 Forbidden - [*] 表示用户得到授权（与401错误相对），但是访问是被禁止的。
404 NOT FOUND - [*]：用户发出的请求针对的是不存在的记录，服务器没有进行操作，该操作是幂等的。
406 Not Acceptable - [GET]：用户请求的格式不可得（比如用户请求JSON格式，但是只有XML格式）。
410 Gone -[GET]：用户请求的资源被永久删除，且不会再得到的。
422 Unprocesable entity - [POST/PUT/PATCH] 当创建一个对象时，发生一个验证错误。
500 INTERNAL SERVER ERROR - [*]：服务器发生错误，用户将无法判断发出的请求是否成功。