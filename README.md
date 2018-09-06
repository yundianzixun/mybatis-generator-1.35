# 简介
大家都知道Mybatis属于半自动ORM，在使用这个框架中，工作量最大的就是书写Mapping的映射文件，并且手动书写很容易出错，那么今天来介绍一下使用Mybatis-Generator来帮我们自动生成文件。如果大家有更好实现方式欢迎留言一起探讨哦，让大家开发起来更爽更便捷~~~

*   源码地址
    *   GitHub：[https://github.com/yundianzixun/mybatis-generator-1.35](https://github.com/yundianzixun/mybatis-generator-1.35)
*   联盟公众号：IT实战联盟
*   我们社区：[https://100boot.cn](https://100boot.cn)

**小工具一枚，欢迎使用和Star支持，如使用过程中碰到问题，可以提出Issue，我会尽力完善该Starter**

#### 第一步：下载mybatis-generator工具包
GitHub地址：https://github.com/yundianzixun/mybatis-generator-1.35，如下图所示：

![mybatis-generator.jpg](https://upload-images.jianshu.io/upload_images/8122772-3a091405101119ef.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

#### 第二步：修改配置信息
##### generatorConfig.xml
```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE generatorConfiguration
  PUBLIC "-//mybatis.org//DTD MyBatis Generator Configuration 1.0//EN"
  "http://mybatis.org/dtd/mybatis-generator-config_1_0.dtd">
<generatorConfiguration>
    <!-- 数据库驱动 -->
    <classPathEntry    location="mysql-connector-java-5.1.9.jar"/>
    <context id="DB2Tables"    targetRuntime="MyBatis3">
        <commentGenerator> 
            <property name="suppressDate" value="true"/>
            <property name="suppressAllComments" value="true"/>
        </commentGenerator>
		<jdbcConnection driverClass="com.mysql.jdbc.Driver"
			connectionURL="数据库URL" userId="数据库用户名" password="数据库密码">
        </jdbcConnection>
		<!-- 数据库类型与java类型转换 -->
        <javaTypeResolver>
            <property name="forceBigDecimals" value="false"/>
        </javaTypeResolver>
        <!-- 生成Model类存放位置 -->
        <javaModelGenerator targetPackage="com.itunion.wxshop.model" targetProject="src">
            <property name="enableSubPackages" value="true"/>
            <property name="trimStrings" value="false"/>
        </javaModelGenerator>
        <!-- 生成映射文件存放位置 -->
        <sqlMapGenerator targetPackage="mapping" targetProject="src">
            <property name="enableSubPackages" value="true"/>
        </sqlMapGenerator>
        <!-- 生成Dao类存放位置 -->
        <javaClientGenerator type="XMLMAPPER" targetPackage="com.itunion.wxshop.mapper" targetProject="src">
            <property name="enableSubPackages" value="true"/>
        </javaClientGenerator>
        <!-- 生成对应表及类名 -->
        <table tableName="user_info" domainObjectName="UserInfo"
               enableCountByExample="false"
               enableUpdateByExample="false"
               enableDeleteByExample="false"
               enableSelectByExample="false"
               selectByExampleQueryId="false">
        </table>
    </context>
</generatorConfiguration>

```

修改点1：数据库配置
```
<jdbcConnection driverClass="com.mysql.jdbc.Driver"
            connectionURL="数据库URL" userId="数据库用户名" password="数据库密码">
        </jdbcConnection>
```

修改点2：生成model类存放位置
```
#com.itunion.wxshop.model 可修改为自己项目映射目录
<javaModelGenerator targetPackage="com.itunion.wxshop.model" targetProject="src">
            <property name="enableSubPackages" value="true"/>
            <property name="trimStrings" value="false"/>
        </javaModelGenerator>
```

修改点3：生成mapping文件存放位置
```
#targetPackage 报名可以修改
<!-- 生成映射文件存放位置 -->
        <sqlMapGenerator targetPackage="mapping" targetProject="src">
            <property name="enableSubPackages" value="true"/>
        </sqlMapGenerator>
```

修改点4：生产Dao类存放位置
```
#targetPackage 目录可修改
<javaClientGenerator type="XMLMAPPER" targetPackage="com.itunion.wxshop.mapper" targetProject="src">
            <property name="enableSubPackages" value="true"/>
        </javaClientGenerator>
```

修改点5：生成对应表及类名
```
#对应自己的表信息（可copy多个）
<table tableName="user_info" domainObjectName="UserInfo"
               enableCountByExample="false"
               enableUpdateByExample="false"
               enableDeleteByExample="false"
               enableSelectByExample="false"
               selectByExampleQueryId="false">
        </table>
```

#### 第三步：控制台执行生成命令（必须要安装好jdk哦）
1. 进入mybatis-generator工具 lib 目录
```
xxx-2:~ lin$ cd /Users/lin/Downloads/JavaCode/mybatis-generator-core-1.3.5wx-shop/lib 
```

2. 执行命令
```
xxx-2:~ lin$ cd /Users/lin/Downloads/JavaCode/mybatis-generator-core-1.3.5wx-shop/lib 
xxx-2:lib lin$ java -jar mybatis-generator-core-1.3.5.jar -configfile generatorConfig.xml -overwrite
MyBatis Generator finished successfully.
xxx-2:lib lin$ 
```
3. 执行结果
```
MyBatis Generator finished successfully.
```
4. 结果查看

![结果.jpg](https://upload-images.jianshu.io/upload_images/8122772-38553edc8caa6ad5.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

#### 第四步：将生成的文件放到自己项目中
generatorConfig.xml 文件里面的项目路径配置好了 直接copy就可以用，如果没有配置好 那么生成的内容还需要手工修改。

## 贡献者
*   [IT实战联盟-Line](https://www.jianshu.com/u/283f93ada597)

#### 关注我们
更多精彩内容请关注“IT实战联盟”哦~~~
![IT实战联盟.jpg](http://upload-images.jianshu.io/upload_images/8122772-8b0153a5719ad830.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/500)
