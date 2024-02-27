> #### 作者主页：[舒克日记](https://blog.csdn.net/cativen)
>
>  简介：Java领域优质创作者、Java项目、学习资料、技术互助
>
> <b><font color=red>文中获取源码</font></b>

# 项目介绍

医院管理系统
分为三个角色 管理员、医生、病人

管理员的主要功能：系统管理、医生管理、患者管理、预约管理、病史管理、住院信息管理、管理员管理
医生的主要功能：就医、查看病史
病人的主要功能：病史、住院信息、挂号

技术框架：
spring boot+spring mvc+mybatis+shrio+jquery+layui+freemarker+bootstrap



# 环境要求

1.运行环境：最好是java jdk1.8,我们在这个平台上运行的。其他版本理论上也可以。 

2.IDE环境：IDEA,Eclipse,Myeclipse都可以。推荐IDEA; 

3.tomcat环境：Tomcat7.x,8.X,9.x版本均可 

4.硬件环境：windows7/8/10 4G内存以上；或者Mac OS; 

5.是否Maven项目：是；查看源码目录中是否包含pom.xml;若包含，则为maven项目，否则为非maven.项目 

6.数据库：MySql5.7/8.0等版本均可；

# 技术栈

后台框架：springboot、MyBatis

数据库：MySQL

环境：JDK8、TOMCAT、IDEA

# 使用说明

1.使用Navicati或者其它工具，在mysql中创建对应sq文件名称的数据库，并导入项目的sql文件； 

2.使用IDEA/Eclipse/MyEclipse导入项目，修改配置，运行项目； 

3.将项目中config-propertiesi配置文件中的数据库配置改为自己的配置，然后运行；

# 运行指导

idea导入源码空间站顶目教程说明(Vindows版)-ssm篇：

http://mtw.so/5MHvZq 

源码地址：[http://codegym.top](http://codegym.top/)。 



# 运行截图
## 登录页
![请添加图片描述](https://img-blog.csdnimg.cn/direct/f18b1cf748634be1876c8adc3013b5b6.png)

## 管理员

![请添加图片描述](https://img-blog.csdnimg.cn/direct/a108042b44e645878abfcd9b9d06ec09.png)

![请添加图片描述](https://img-blog.csdnimg.cn/direct/9885bb8f69b844d18689f0682f0b4aee.png)
![请添加图片描述](https://img-blog.csdnimg.cn/direct/169ea5efa23c4a1fbc2f7e77e87ffd71.png)
![请添加图片描述](https://img-blog.csdnimg.cn/direct/d9ee158c8cdb43e9b1aa5676899bdd66.png)
![请添加图片描述](https://img-blog.csdnimg.cn/direct/bcb4755e86c3494d9337ad7cf85b11d9.png)
## 医生
![请添加图片描述](https://img-blog.csdnimg.cn/direct/5b71c27a3a414c34b9b2d5befda0a4d4.png)
## 患者
![请添加图片描述](https://img-blog.csdnimg.cn/direct/d073df2609644b24bf476e353195cac2.png)
![请添加图片描述](https://img-blog.csdnimg.cn/direct/bf7d2f25102e428b9f4542440081bbd0.png)
# 代码
MySessionManager

```
package com.gbq.hospital.config.shiro;

import com.github.pagehelper.util.StringUtil;
import org.apache.shiro.web.servlet.ShiroHttpServletRequest;
import org.apache.shiro.web.session.mgt.DefaultWebSessionManager;

import javax.servlet.ServletRequest;
import javax.servlet.ServletResponse;
import javax.servlet.http.HttpServletRequest;
import java.io.Serializable;

/**
 * @author Morty
 */
public class MySessionManager extends DefaultWebSessionManager {

    public static final String AUTHORIZATION = "token";

    public static final String REFERENCED_SESSION_ID_SOURCE = "Stateless request";

    public MySessionManager() {
        super();
    }

    @Override
    protected Serializable getSessionId(ServletRequest request, ServletResponse response) {
        HttpServletRequest httpServletRequest = (HttpServletRequest) request;
        String sessionId = httpServletRequest.getHeader(AUTHORIZATION);
        //如果请求头中有 Authorization 则其值为sessionId
        if (StringUtil.isNotEmpty(sessionId)) {
            request.setAttribute(ShiroHttpServletRequest.REFERENCED_SESSION_ID_SOURCE, REFERENCED_SESSION_ID_SOURCE);
            request.setAttribute(ShiroHttpServletRequest.REFERENCED_SESSION_ID, sessionId);
            request.setAttribute(ShiroHttpServletRequest.REFERENCED_SESSION_ID_IS_VALID, Boolean.TRUE);
            return sessionId;
        } else {
            //否则按默认规则从cookie取sessionId
            return super.getSessionId(request, response);
        }

    }
}
```
