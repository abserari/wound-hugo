+++
author = "Abser"
categories = ["Gorm"]
date = "2018-11-11"
description = "Learn how to create service by Gin and Gorm"
featured = "pic01.jpg"
featuredalt = "Pic 1"
featuredpath = "date"
linktitle = ""
title = "Create A Service By Gin-Gorm"
type = "post"

+++


<span data-type="color" style="color:rgb(47, 47, 47)"><span data-type="background" style="background-color:rgb(255, 255, 255)">原文链接：</span></span>[https://medium.com/@cgrant/developing-a-simple-crud-api-with-go-gin-and-gorm-df87d98e6ed1](https://link.jianshu.com/?t=https%3A%2F%2Fmedium.com%2F%40cgrant%2Fdeveloping-a-simple-crud-api-with-go-gin-and-gorm-df87d98e6ed1)
翻译：<span data-type="color" style="color:rgb(47, 47, 47)"><span data-type="background" style="background-color:rgb(255, 255, 255)">devabel</span></span>
整理：abser
## 入门

这个例子假设你已经安装并运行go语言的环境。如果您还没有安装，请转到[http://cgrant.io/tutorials/go/getting-started-with-go/](https://link.jianshu.com?t=http%3A%2F%2Fcgrant.io%2Ftutorials%2Fgo%2Fgetting-started-with-go%2F)获取快速入门。

### Gin Web框架

由于我们将通过HTTP提供我们的API，因此我们需要一个Web框架来处理路由并提供请求。有许多框架可用，具有不同的功能和性能指标。在这个例子中，我们将使用Gin框架[https://github.com/gin-gonic/gin](https://link.jianshu.com?t=https%3A%2F%2Fgithub.com%2Fgin-gonic%2Fgin)  。由于速度和简单性，Gin是API开发的一个很好的框架。

首先，让我们在`$ GOPATH / src / simple-api`中为我们的服务创建一个新文件夹，然后添加一个main.go文件，如下所示

```go
package main

import “fmt”

func main() {
 fmt.Println(“Hello World”)
}
```

在我们继续学习前，让我们测试一下，确保一切正常运行。

```go
$ go run main.go
Hello World
```
程序运行正常。现在让我们使用Gin框架将它变成一个Web应用程序。

```go
package main

import “github.com/gin-gonic/gin”

func main() {
 r := gin.Default()
 r.GET(“/”, func(c *gin.Context) {
 c.String(200, “Hello World”)
 })
 r.Run() 
}
```

保存并运行它

```go
$ go run main.go
[GIN-debug] [WARNING] Running in “debug” mode. Switch to “release” mode in production.
 — using env: export GIN_MODE=release
 — using code: gin.SetMode(gin.ReleaseMode)

[GIN-debug] GET / → main.main.func1 (3 handlers)
[GIN-debug] Environment variable PORT is undefined. Using port :8080 by default
[GIN-debug] Listening and serving HTTP on :8080
[GIN] 2016/12/02–14:57:52 | 200 | 33.798µs | ::1 | GET /
```

然后浏览器访问[http://localhost:8080/](https://link.jianshu.com?t=http%3A%2F%2Flocalhost%3A8080%2F)

```plain
Hello World
```

成功！！！

我们正在构建一个API，但不是一个Web应用程序，所以让我们将其切换到JSON响应

```go
package main

import “github.com/gin-gonic/gin”

func main() {
    r := gin.Default()
    r.GET(“/”, func(c *gin.Context) {
        c.JSON(200, gin.H{
        “message”: “Hello World”,
        })
    })
 r.Run() // listen and server on 0.0.0.0:8080
}
```

保存文件，重新运行并刷新浏览器，您应该看到我们的JSON 消息
`{“message”：“Hello World”}`

### GORM的数据持久性

现在让我们看看我们的持久层。对于本节我们将使用本地的基于SQLite文件的数据库开始。稍后我们将切换到使用MySql来证明。

Gorm [http://jinzhu.me/gorm/](https://link.jianshu.com?t=http%3A%2F%2Fjinzhu.me%2Fgorm%2F)是一个用于go的对象关系映射（ORM）框架。它大大简化了模型到数据库的映射和持久化。尽管我不是大型复杂系统的ORM的忠实拥趸，但他们对原型开发新的绿地应用程序确实很有效。Gorm在Go领域是一个非常受欢迎的工具，我们将在这里看看它。

为了解决gorm问题，我们将把我们刚写的Gin代码换掉，并且演示一下gorm的功能。学习完这块，我们会将Gin重新添加到应用程序中。

让我们开始一个小例子。

```go
package main

import (
 “github.com/jinzhu/gorm”
 _ “github.com/jinzhu/gorm/dialects/sqlite”
)

func main() {
 db, _ := gorm.Open(“sqlite3”, “./gorm.db”)
 defer db.Close()

}
```

如果你现在运行这个程序，你会在你的文件系统中看到一个名为gorm.db的新文件。这是我们的数据库文件系统将在应用程序中使用。虽然我们可以看到我们的应用程序正在运行，而且gorm正在被使用，但我们的系统还没有完成。让我们添加更多的代码。

```go
package main

import (
 “fmt”

“github.com/jinzhu/gorm”
 _ “github.com/jinzhu/gorm/dialects/sqlite”
)

type Person struct {
 ID uint `json:”id”`
 FirstName string `json:”firstname”`
 LastName string `json:”lastname”`
}

func main() {
 db, _ := gorm.Open(“sqlite3”, “./gorm.db”)
 defer db.Close()

 p1 := Person{FirstName: “John”, LastName: “Doe”}
 p2 := Person{FirstName: “Jane”, LastName: “Smith”}

 fmt.Println(p1.FirstName)
 fmt.Println(p2.LastName)

}
```

在这里，我们刚刚添加了一个简单的Person结构，并在使用它们打印出值之前创建了一些实例。请记住，Person结构中的字段需要以大写字母开头，因为Go定义这些是公共字段。

现在我们已经有了一个可以使用Gorm的对象。

```go
package main

import (
 “fmt”

“github.com/jinzhu/gorm”
 _ “github.com/jinzhu/gorm/dialects/sqlite”
)

type Person struct {
 ID uint `json:”id”`
 FirstName string `json:”firstname”`
 LastName string `json:”lastname”`
}

func main() {
 db, _ := gorm.Open(“sqlite3”, “./gorm.db”)
 defer db.Close()

 db.AutoMigrate(&Person{})

 p1 := Person{FirstName: “John”, LastName: “Doe”}
 p2 := Person{FirstName: “Jane”, LastName: “Smith”}

 db.Create(&p1)
 var p3 Person // identify a Person type for us to store the results in
 db.First(&p3) // Find the first record in the Database and store it in p3

 fmt.Println(p1.FirstName)
 fmt.Println(p2.LastName)
 fmt.Println(p3.LastName) // print out our record from the database

}
```

现在让我们运行它，看看输出什么


```go
$ go run main.go
John
Smith
Doe
```

哇，非常简单。只需几行代码，我们就可以保存并从数据库中检索。Gorm在如何存储和查询他们的网站上有更多的选项。接下来我们将介绍几个核心部分，但请查看他们的文档以获取更多选项。

## API框架

我们已经回顾了框架如何独立运作。现在是时候把所有东西放在一起成为一个可用的API

### 查询所有信息

让我们从查阅我们之前添加的数据开始阅读CRUD的部分。我将删除我们刚刚通过的一些行，并用一个新路由添加到Gin框架中，以查询我们的数据库。

```go
package main

import (
 “fmt”

 “github.com/gin-gonic/gin”
 “github.com/jinzhu/gorm”
 _ “github.com/jinzhu/gorm/dialects/sqlite”
)

var db *gorm.DB
var err error

type Person struct {
 ID uint `json:”id”`
 FirstName string `json:”firstname”`
 LastName string `json:”lastname”`
}

func main() {

 // NOTE: See we’re using = to assign the global var
 // instead of := which would assign it only in this function
 db, err = gorm.Open(“sqlite3”, “./gorm.db”)
 if err != nil {
   fmt.Println(err)
 }
 defer db.Close()

 db.AutoMigrate(&Person{})

 r := gin.Default()
 r.GET(“/”, GetProjects)

 r.Run(“:8080”)
}

func GetProjects(c *gin.Context) {
 var people []Person
 if err := db.Find(&people).Error; err != nil {
    c.AbortWithStatus(404)
    fmt.Println(err)
 } else {
    c.JSON(200, people)
 }

}
```

现在运行它并转到[http://localhost:8080/](https://link.jianshu.com?t=http%3A%2F%2Flocalhost%3A8080%2F)，你应该看到

```
[{“id”: 1,”firstname”: “John”,”lastname”: “Doe”}]
```

哇只是几行代码，我们已经获得API响应。大部分都是错误处理！

### 查询单条信息

OK让我们以REST为导向更新上下文，并增加查找单条信息的功能。

```go
package main

import (
 “fmt”

 “github.com/gin-gonic/gin”
 “github.com/jinzhu/gorm”
 _ “github.com/jinzhu/gorm/dialects/sqlite”
)

var db *gorm.DB
var err error

type Person struct {
 ID uint `json:”id”`
 FirstName string `json:”firstname”`
 LastName string `json:”lastname”`
}

func main() {

 // NOTE: See we’re using = to assign the global var
 // instead of := which would assign it only in this function
 db, err = gorm.Open(“sqlite3”, “./gorm.db”)
 if err != nil {
    fmt.Println(err)
 }
 defer db.Close()

 db.AutoMigrate(&Person{})

 r := gin.Default()
 r.GET(“/people/”, GetPeople)
 r.GET(“/people/:id”, GetPerson)

 r.Run(“:8080”)
}

func GetPerson(c *gin.Context) {
 id := c.Params.ByName(“id”)
 var person Person
 if err := db.Where(“id = ?”, id).First(&person).Error; err != nil {
    c.AbortWithStatus(404)
    fmt.Println(err)
 } else {
    c.JSON(200, person)
 }
}

func GetPeople(c *gin.Context) {
 var people []Person
 if err := db.Find(&people).Error; err != nil {
 c.AbortWithStatus(404)
    fmt.Println(err)
 } else {
    c.JSON(200, people)
 }

}
```

现在运行服务器，但请注意，我们更改了上下文，现在您将转到http：// localhost：8080 / people /查看您的列表。一旦将该ID添加到网址的末尾，您将得到单个记录返回http：// localhost：8080 / people / 1

```
$ go run main.go
John
Smith
Doe
```

哇，非常简单。只需几行代码，我们就可以保存并从数据库中检索。Gorm在如何存储和查询他们的网站上有更多的选项。接下来我们将介绍几个核心部分，但请查看他们的文档以获取更多选项。

## 制作API

我们已经回顾了框架如何独立运作。现在是时候把所有东西放在一起成为一个可用的API

### 查询所有信息

让我们从查阅我们之前添加的数据开始阅读CRUD的部分。我将删除我们刚刚通过的一些行，并用一个新路由添加到Gin框架中，以查询我们的数据库。

```go
package main

import (
 “fmt”

 “github.com/gin-gonic/gin”
 “github.com/jinzhu/gorm”
 _ “github.com/jinzhu/gorm/dialects/sqlite”
)

var db *gorm.DB
var err error

type Person struct {
 ID uint `json:”id”`
 FirstName string `json:”firstname”`
 LastName string `json:”lastname”`
}

func main() {

 // NOTE: See we’re using = to assign the global var
 // instead of := which would assign it only in this function
 db, err = gorm.Open(“sqlite3”, “./gorm.db”)
 if err != nil {
   fmt.Println(err)
 }
 defer db.Close()

 db.AutoMigrate(&Person{})

 r := gin.Default()
 r.GET(“/”, GetProjects)

 r.Run(“:8080”)
}

func GetProjects(c *gin.Context) {
 var people []Person
 if err := db.Find(&people).Error; err != nil {
    c.AbortWithStatus(404)
    fmt.Println(err)
 } else {
    c.JSON(200, people)
 }

}
```

现在运行它并转到[http://localhost:8080/](https://link.jianshu.com?t=http%3A%2F%2Flocalhost%3A8080%2F)，你应该看到

```
[{“id”: 1,”firstname”: “John”,”lastname”: “Doe”}]
```

哇只是几行代码，我们已经获得API响应。大部分都是错误处理！

### 查询单条信息

OK让我们以REST为导向更新上下文，并增加查找单条信息的功能。

```go
package main

import (
 “fmt”

 “github.com/gin-gonic/gin”
 “github.com/jinzhu/gorm”
 _ “github.com/jinzhu/gorm/dialects/sqlite”
)

var db *gorm.DB
var err error

type Person struct {
 ID uint `json:”id”`
 FirstName string `json:”firstname”`
 LastName string `json:”lastname”`
}

func main() {

 // NOTE: See we’re using = to assign the global var
 // instead of := which would assign it only in this function
 db, err = gorm.Open(“sqlite3”, “./gorm.db”)
 if err != nil {
    fmt.Println(err)
 }
 defer db.Close()

 db.AutoMigrate(&Person{})

 r := gin.Default()
 r.GET(“/people/”, GetPeople)
 r.GET(“/people/:id”, GetPerson)

 r.Run(“:8080”)
}

func GetPerson(c *gin.Context) {
 id := c.Params.ByName(“id”)
 var person Person
 if err := db.Where(“id = ?”, id).First(&person).Error; err != nil {
    c.AbortWithStatus(404)
    fmt.Println(err)
 } else {
    c.JSON(200, person)
 }
}

func GetPeople(c *gin.Context) {
 var people []Person
 if err := db.Find(&people).Error; err != nil {
 c.AbortWithStatus(404)
    fmt.Println(err)
 } else {
    c.JSON(200, people)
 }

}
```

现在运行服务器，但请注意，我们更改了上下文，现在您将转到http：// localhost：8080 / people /查看您的列表。一旦将该ID添加到网址的末尾，您将得到单个记录返回http：// localhost：8080 / people / 1


```json
{“id”: 1,”firstname”: “John”,”lastname”: “Doe”}
```

### 创建

很难用仅有一条记录来看出差异。很难区分[{...}]和{...}之间的区别所以让我们添加Create函数和路由

```go
package main

import (
 “fmt”

 “github.com/gin-gonic/gin”
 “github.com/jinzhu/gorm”
 _ “github.com/jinzhu/gorm/dialects/sqlite”
)

var db *gorm.DB
var err error

type Person struct {
 ID uint `json:”id”`
 FirstName string `json:”firstname”`
 LastName string `json:”lastname”`
}

func main() {

 // NOTE: See we’re using = to assign the global var
 // instead of := which would assign it only in this function
 db, err = gorm.Open(“sqlite3”, “./gorm.db”)
 if err != nil {
 fmt.Println(err)
 }
 defer db.Close()

db.AutoMigrate(&Person{})

 r := gin.Default()
 r.GET(“/people/”, GetPeople)
 r.GET(“/people/:id”, GetPerson)
 r.POST(“/people”, CreatePerson)

r.Run(“:8080”)
}

func CreatePerson(c *gin.Context) {

 var person Person
 c.BindJSON(&person)

 db.Create(&person)
 c.JSON(200, person)
}

func GetPerson(c *gin.Context) {
 id := c.Params.ByName(“id”)
 var person Person
 if err := db.Where(“id = ?”, id).First(&person).Error; err != nil {
    c.AbortWithStatus(404)
    fmt.Println(err)
 } else {
    c.JSON(200, person)
 }
}

func GetPeople(c *gin.Context) {
 var people []Person
 if err := db.Find(&people).Error; err != nil {
    c.AbortWithStatus(404)
    fmt.Println(err)
 } else {
    c.JSON(200, people)
 }

}
```

现在要测试这一个，我们将从命令行运行一个curl命令。我们还需要运行服务器，以便打开另一个终端窗口，以便可以运行这两个命令。使用\$ go run main.go在第一个窗口中运行服务器

一旦运行，在第二个窗口运行：

```basic
$ curl -i -X POST http://localhost:8080/people -d ‘{ “FirstName”: “Elvis”, “LastName”: “Presley”}’
```

你应该看到一个成功的回应

```basic
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
Date: Sat, 03 Dec 2016 00:14:06 GMT
Content-Length: 50

{“id”:2,”firstname”:”Elvis”,”lastname”:”Presley”}
```

现在让我们在浏览器中列出我们的人员，看看它是否列出了我们所有的条目
`http：// localhost：8080 / people /`

```json
[{“id”: 1,”firstname”: “John”,”lastname”: “Doe”},{“id”: 2,”firstname”: “Elvis”,”lastname”: “Presley”}]
```

太棒了，输出结果！看到这里你认为这很酷。

这次只发送部分Person数据

```basic
$ curl -i -X POST [http://localhost:8080/people](http://localhost:8080/people) -d ‘{ “FirstName”: “Madison”}’
```
刷新浏览器并查看它只添加了我们发送的数据

```json
[{“id”: 1,”firstname”: “John”,”lastname”: “Doe”},{“id”: 2,”firstname”: “Elvis”,”lastname”: “Presley”},{“id”: 3,”firstname”: “Madison”,”lastname”: “”}]
```

这是Gin的一部分，请注意CreatePerson函数中的c.BindJSON（＆person）行。它会自动填充请求中的任何匹配数据字段。

<span data-type="background" style="background-color:#FADB14">你也可能错过了它，但我的数据库中的情况和我通过的情况是不同的。Gin 对大小写不敏感。我传入了FirstName ，但数据库使用了firstname.。</span>

很简单！

### 更新

尽管如此，我们不能让Madison的last name为空。是时候添加我们的更新功能了

```go
package main

import (
 “fmt”

 “github.com/gin-gonic/gin”
 “github.com/jinzhu/gorm”
 _ “github.com/jinzhu/gorm/dialects/sqlite”
)

var db *gorm.DB
var err error

type Person struct {
 ID uint `json:”id”`
 FirstName string `json:”firstname”`
 LastName string `json:”lastname”`
}

func main() {

 // NOTE: See we’re using = to assign the global var
 // instead of := which would assign it only in this function
 db, err = gorm.Open(“sqlite3”, “./gorm.db”)
 if err != nil {
    fmt.Println(err)
 }
 defer db.Close()

 db.AutoMigrate(&Person{})

 r := gin.Default()
 r.GET(“/people/”, GetPeople)
 r.GET(“/people/:id”, GetPerson)
 r.POST(“/people”, CreatePerson)
 r.PUT(“/people/:id”, UpdatePerson)

 r.Run(“:8080”)
}

func UpdatePerson(c *gin.Context) {

 var person Person
 id := c.Params.ByName(“id”)

 if err := db.Where(“id = ?”, id).First(&person).Error; err != nil {
    c.AbortWithStatus(404)
    fmt.Println(err)
 }
 c.BindJSON(&person)

 db.Save(&person)
 c.JSON(200, person)

}

func CreatePerson(c *gin.Context) {

 var person Person
 c.BindJSON(&person)

 db.Create(&person)
 c.JSON(200, person)
}

func GetPerson(c *gin.Context) {
 id := c.Params.ByName(“id”)
 var person Person
 if err := db.Where(“id = ?”, id).First(&person).Error; err != nil {
    c.AbortWithStatus(404)
    fmt.Println(err)
 } else {
    c.JSON(200, person)
 }
}

func GetPeople(c *gin.Context) {
 var people []Person
 if err := db.Find(&people).Error; err != nil {
    c.AbortWithStatus(404)
    fmt.Println(err)
 } else {
    c.JSON(200, people)
 }

}
```

为了测试这个，我们将使用一个类似的curl命令，但是我们会在特定的用户上调用PUT方法

```basic
$ curl -i -X PUT http://localhost:8080/people/3 -d ‘{ “FirstName”: “Madison”, “LastName”:”Sawyer” }’
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
Date: Sat, 03 Dec 2016 00:25:35 GMT
Content-Length: 51

{“id”:3,”firstname”:”Madison”,”lastname”:”Sawyer”}
```

果然，如果我们刷新我们的浏览器，我们看到它添加了Sawyer这条数据。

```json
[{“id”: 1,”firstname”: “John”,”lastname”: “Doe”},{“id”: 2,”firstname”: “Elvis”,”lastname”: “Presley”},{“id”: 3,”firstname”: “Madison”,”lastname”: “Sawyer”}]
```

我们再次可以发送部分数据进行部分更新

```basic
$ curl -i -X PUT http://localhost:8080/people/3 -d ‘{ “FirstName”: “Tom” }’
```

显示为

```json
[{“id”: 1,”firstname”: “John”,”lastname”: “Doe”},{“id”: 2,”firstname”: “Elvis”,”lastname”: “Presley”},{“id”: 3,”firstname”: “Tom”,”lastname”: “Sawyer”}]
```

### 删除

```go
package main

import (
 “fmt”

 “github.com/gin-gonic/gin”
 “github.com/jinzhu/gorm”
 _ “github.com/jinzhu/gorm/dialects/sqlite”
)

var db *gorm.DB
var err error

type Person struct {
 ID uint `json:”id”`
 FirstName string `json:”firstname”`
 LastName string `json:”lastname”`
}

func main() {

 // NOTE: See we’re using = to assign the global var
 // instead of := which would assign it only in this function
 db, err = gorm.Open(“sqlite3”, “./gorm.db”)
 if err != nil {
    fmt.Println(err)
 }
 defer db.Close()

 db.AutoMigrate(&Person{})

 r := gin.Default()
 r.GET(“/people/”, GetPeople)
 r.GET(“/people/:id”, GetPerson)
 r.POST(“/people”, CreatePerson)
 r.PUT(“/people/:id”, UpdatePerson)
 r.DELETE(“/people/:id”, DeletePerson)

 r.Run(“:8080”)
}

func DeletePerson(c *gin.Context) {
 id := c.Params.ByName(“id”)
 var person Person
 d := db.Where(“id = ?”, id).Delete(&person)
 fmt.Println(d)
 c.JSON(200, gin.H{“id #” + id: “deleted”})
}

func UpdatePerson(c *gin.Context) {

 var person Person
 id := c.Params.ByName(“id”)

 if err := db.Where(“id = ?”, id).First(&person).Error; err != nil {
    c.AbortWithStatus(404)
    fmt.Println(err)
 }
 c.BindJSON(&person)

 db.Save(&person)
 c.JSON(200, person)

}

func CreatePerson(c *gin.Context) {

 var person Person
 c.BindJSON(&person)

 db.Create(&person)
 c.JSON(200, person)
}

func GetPerson(c *gin.Context) {
 id := c.Params.ByName(“id”)
 var person Person
 if err := db.Where(“id = ?”, id).First(&person).Error; err != nil {
    c.AbortWithStatus(404)
    fmt.Println(err)
 } else {
    c.JSON(200, person)
 }
}

func GetPeople(c *gin.Context) {
 var people []Person
 if err := db.Find(&people).Error; err != nil {
    c.AbortWithStatus(404)
    fmt.Println(err)
 } else {
    c.JSON(200, people)
 }

}
```
为了测试这个，我们将使用带curl的Delete方法来调用它

```basic
$ curl -i -X DELETE http://localhost:8080/people/1

HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
Date: Sat, 03 Dec 2016 00:32:40 GMT
Content-Length: 20

{“id #1”:”deleted”}
```

刷新浏览器，你会看到我们的John Doe已被删除

```json
[{“id”: 2,”firstname”: “Elvis”,”lastname”: “Presley”},{“id”: 3,”firstname”: “Tom”,”lastname”: “Sawyer”}]
```

## 修改模型

在定义基本的API后，现在是开始改变Person对象的好时机。我们可以通过只更改person结构来轻松修改数据库和api。

我要做的就是在Person Struct中添加一个city字段。没有其他的，就一行。

```go
type Person struct {
 ID uint `json:”id”`
 FirstName string `json:”firstname”`
 LastName string `json:”lastname”`
 City string `json:”city”`
}
```

刷新我们的浏览器并拉出列表，您可以看到我所有的对象现在都有city

```json
[{“id”: 2,”firstname”: “Elvis”,”lastname”: “Presley”,”city”: “”},{“id”: 3,”firstname”: “Tom”,”lastname”: “Sawyer”,”city”: “”}]
```

我可以创建并更新新字段，而无需进行其他更改

```basic
$ curl -i -X PUT http://localhost:8080/people/2 -d ‘{ “city”: “Memphis” }’
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
Date: Sat, 03 Dec 2016 00:40:57 GMT
Content-Length: 67

{“id”:2,”firstname”:”Elvis”,”lastname”:”Presley”,”city”:”Memphis”}
```

这全部由我们主函数中的db.AutoMigrate（＆Person {}）行处理。在生产环境中，我们希望更接近地管理架构，但对于原型来说，这是完美的

# 使用MySql

好的，我明白，没问题，你想使用MySql而不是SQLite。

为此，我们只需要修改一个导入声明和连接..

导入\_“github.com/go-sql-driver/mysql”

连接

```go
db, _ = gorm.Open(“mysql”, “user:pass@tcp(127.0.0.1:3306)/samples?charset=utf8&parseTime=True&loc=Local”)
```

完整的例子

```go
package main

// only need mysql OR sqlite 
// both are included here for reference
import (
 “fmt”

 “github.com/gin-gonic/gin”
 _ “github.com/go-sql-driver/mysql” 
 “github.com/jinzhu/gorm”
 _ “github.com/jinzhu/gorm/dialects/sqlite”
)

var db *gorm.DB
var err error

type Person struct {
 ID uint `json:”id”`
 FirstName string `json:”firstname”`
 LastName string `json:”lastname”`
 City string `json:”city”`
}

func main() {

 // NOTE: See we’re using = to assign the global var
 // instead of := which would assign it only in this function
 //db, err = gorm.Open(“sqlite3”, “./gorm.db”)
 db, _ = gorm.Open(“mysql”, “user:pass@tcp(127.0.0.1:3306)/database?charset=utf8&parseTime=True&loc=Local”)

 if err != nil {
    fmt.Println(err)
 }
 defer db.Close()

 db.AutoMigrate(&Person{})

 r := gin.Default()
 r.GET(“/people/”, GetPeople)
 r.GET(“/people/:id”, GetPerson)
 r.POST(“/people”, CreatePerson)
 r.PUT(“/people/:id”, UpdatePerson)
 r.DELETE(“/people/:id”, DeletePerson)

 r.Run(“:8080”)
}

func DeletePerson(c *gin.Context) {
 id := c.Params.ByName(“id”)
 var person Person
 d := db.Where(“id = ?”, id).Delete(&person)
 fmt.Println(d)
 c.JSON(200, gin.H{“id #” + id: “deleted”})
}

func UpdatePerson(c *gin.Context) {

 var person Person
 id := c.Params.ByName(“id”)

 if err := db.Where(“id = ?”, id).First(&person).Error; err != nil {
    c.AbortWithStatus(404)
    fmt.Println(err)
 }
 c.BindJSON(&person)

 db.Save(&person)
 c.JSON(200, person)

}

func CreatePerson(c *gin.Context) {

 var person Person
 c.BindJSON(&person)

 db.Create(&person)
 c.JSON(200, person)
}

func GetPerson(c *gin.Context) {
 id := c.Params.ByName(“id”)
 var person Person
 if err := db.Where(“id = ?”, id).First(&person).Error; err != nil {
    c.AbortWithStatus(404)
    fmt.Println(err)
 } else {
    c.JSON(200, person)
 }
}

func GetPeople(c *gin.Context) {
 var people []Person
 if err := db.Find(&people).Error; err != nil {
    c.AbortWithStatus(404)
    fmt.Println(err)
 } else {
    c.JSON(200, people)
 }

}
```


