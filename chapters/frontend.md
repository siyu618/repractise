#前端

###什么是前端？

维基百科是这样说的：前端Front-end和后端back-end是描述进程开始和结束的通用词汇。前端作用于采集输入信息，后端进行处理。计算机程序的界面样式，视觉呈现属于前端。

这种的说法给人一种很模糊的感觉，但是他说得又很对，它负责视觉展示。在MVC结构或者MVP中，负责视觉显示的部分只有View层，而今天大多数所谓的View层已经超越了View层。View层是一个很神奇的概念，但是而今的View层已经发现了很大的变化。

你引入了React、Backbone、Angluar，你的架构变成了MVVM、MVP、MVC。尽管发生了一些架构上的变化，但是项目的开发并没有因此而发生变化。这其中涉及到了一些职责的问题，如果某一个层级中有太多的职责，那么它是不是加重了一些人的负担。

##前端发展的历史

过去一直想整理一篇文章来说说前端发展的历史，但是想了想这些历史已经被人们所熟知。后来发现并非如此，只是因为关注的一些人都是有历史的，后来发现事情并非如此。

###数据-模板-样式混合

在有限的前端经验里，我还是经历了那段用Table来作样式的年代。大学期间曾经有偿帮一些公司或者个人维护、开发一些CMS，而Table是当时帮某个网站更新样式接触到的——ASP.Net（maybe)。当时，我们启动这个CMS，用的是一个名为``aspweb.exe``的程序。于是，在我的移动硬盘里找到了下面的代码。

```html
<TABLE cellSpacing=0 cellPadding=0 width=910 align=center border=0>
  <TBODY>
  <TR>
    <TD vAlign=top width=188><TABLE cellSpacing=0 cellPadding=0 width=184 align=center border=0>
        <TBODY>
        <TR>
          <TD><IMG src="Images/xxx.gif" width=184></TD></TR>
        <TR>
          <TD>
            <TABLE cellSpacing=0 cellPadding=0 width=184 align=center 
            background=Images/xxx.gif border=0>
```            

虽然，我也已经在HEAD里找到了现代的雏形——DIV + CSS，而这还是一个Table的年代。

```html
<LINK href="img/xxx.css" type=text/css rel=stylesheet>
```

**人们一直在说前端很难，问题是你学过么！！！**也许，你也一直在说CSS不好写，但是CSS真的不好写么？人们总在说JS很难用，但是你学过么？只在用的时候才去学，那肯定很难。**你不曾花时间去学习一门语言，但是却能直接写出可以work的代码，正是在说明他们容易上手么？**如果你看过一些有经验的Ruby、Scala、Emacs Lisp开发者写出来的代码，我想会得到相同的结论。有一些语言可以使写程序的人Happy，但是看的人可能就不会Happy。做事的方法不止一种，但是不是所有的人都要用那种方法去做。

过去的那些程序员都是**真正的全栈程序员**，这些程序员不仅仅做了前端的活，然后还有数据库的工作。

```asp
Set rs = Server.CreateObject("ADODB.Recordset")
sql = "select id,title,username,email,qq,adddate,content,Re_content,home,face,sex from Fl_Book where ispassed=1 order by id desc"
rs.open sql, Conn, 1, 1
fl.SqlQueryNum = fl.SqlQueryNum + 1
```

在这个ASP文件里，它从数据库里查找出了数据，然后Render出HTML。如果可以看到版本的历史，那么我想我会看到有一个作者将style=""的代码一个个放到css文件中。

在这里的代码里也免不了有动态生成JavaScript代码的方法：

```asp
show_other = "<SCRIPT language=javascript>"
show_other = show_other & "function checkform()"
show_other = show_other & "{"
show_other = show_other & "if (document.add.title.value=='')"
show_other = show_other & "{"
```

请尽情嘲笑，然后再看段代码：

```javascript
import React from "react";
import { getData } from "../../common/request";
import styles from "./style.css";


export default class HomePage extends React.Component {
  componentWillMount() {
    console.log("[HomePage] will mount with server response: ", this.props.data.home);
  }

  render() {
    let { title } = this.props.data.home;

    return (
      <div className={styles.content}>
        <h1>{title}</h1>
        <p className={styles.welcomeText}>Thanks for joining!</p>
      </div>
    );
  }

  static fetchData = function(params) {
    return getData("/home");
  }
}
```

10年前和10年后的代码，似乎没有太多的变化。有所不同的是数据层已经被独立出去了，如果你的component也混合了数据层，即直接查询数据库而不是调用数据层接口，那么你就需要好好思考下这个问题。你只是在追随潮流，还是在改变。用一个View层更换一个View层，用一个Router换一个Router的意义在哪？

###Model-View-Controller

人们在不断地反思这其中复杂的过程，整理了一些好的架构模式，其中不得不提到的是我司Martin Folwer的《企业应用架构模式》。这本书译版出版的时候是2004年，那时对于系统的分层是

层次	   | 职责
-------| -----
表现层  | 	提供服务、显示信息、用户请求、HTTP请求和命令行调用。
领域层  | 	逻辑处理，系统中真正的核心。
数据层  | 	与数据库、消息系统、事物管理器和其他软件包通讯。

化身于当时最流行的Spring，就是MVC。人们有了iBatis这样的数据持久层框架，即ORM，对象关系映射。于是，你的package就会有这样的几个文件夹：

```
|____mappers
|____model
|____service
|____utils
|____controller
```

在mappers这一层，我们所做的莫过于如下所示的数据库相关查询：

```java
@Insert(
        "INSERT INTO users(username, password, enabled) " +
                "VALUES (#{userName}, #{passwordHash}, #{enabled})"
)
@Options(keyProperty = "id", keyColumn = "id", useGeneratedKeys = true)
void insert(User user);
```    

model文件夹和mappers文件夹都是数据层的一部分，只是两者间的职责不同，如：

```java
public String getUserName() {
    return userName;
}

public void setUserName(String userName) {
    this.userName = userName;
}
```

而他们最后都需要在Controller，又或者称为ModelAndView中处理：

```java
@RequestMapping(value = {"/disableUser"}, method = RequestMethod.POST)
public ModelAndView processUserDisable(HttpServletRequest request, ModelMap model) {
    String userName = request.getParameter("userName");
    User user = userService.getByUsername(userName);
    userService.disable(user);
    Map<String,User> map = new HashMap<String,User>();
    Map <User,String> usersWithRoles= userService.getAllUsersWithRole();
    model.put("usersWithRoles",usersWithRoles);
    return new ModelAndView("redirect:users",map);
}
```

在多数时候，Controller不应该直接与数据层的一部分，而将业务逻辑放在Controller层又是一种错误，这时就会有Service层。就有了下图：

![Service MVC](img/frontend/service-mvc.png)

然而，人们对于Service应该放在哪一层都有不同意见：

![MS Player](img/frontend/mvcplayer.gif)
![MS MVC](img/frontend/ms-mvc.png)

最后，我们的View层出现了，