# SJRSAEncryptor
Test update open source file to cocoapods.

![](http://oqepgj2jp.bkt.clouddn.com/cocoapods.png)

####  一、前言
如何将自己写的`Github`上的代码添加`Cocoapods`支持，此文将以一个[iOS RSA](https://github.com/CoderSteveJones/SJRSAEncryptor.git)加密库文件为例，讲述整个过程。

#### 二、步骤
这里我将从最初的开始进行介绍，包括`Github`上创建项目已经上传项目，到最后的支持`Cocoapods`。
步骤如下：
- 代码上传`Github`
- 创建`podspec`文件，并验证是否通过
- 在`Github`上创建`release`版本
- 注册`CocoaPods`账号
- 上传代码到`CocoaPods`
- 检查上传是否成功

##### 1 代码上传Github
首先我们打开[github.com](https://github.com/)，然后创建自己的项目工程：
![图一](http://oqepgj2jp.bkt.clouddn.com/cocoapods1.png)


这里注意那个`MIT License`，在后面添加`Cocoapods`支持的时候会用到（稍后介绍）。然后点击创建即可。
然后用`SouceTree`将代码`down`到本地，将自己的项目放到里面，文件夹如图所示：


![图二.png](http://oqepgj2jp.bkt.clouddn.com/cocoapods2.png)

这里的`LICENSE`就是刚才说的`MIT License`添加的文件。`SJRSAEncryptorDemo`是示例工程，`SJRSAEncryptor`就是提供给他人使用的库。然后提交到`Github`就可以了。

#####  2 创建podspec文件
我们使用终端到工程目录下：

执行:
```
pod spec create SJRSAEncryptor   // SJRSAEncryptor改为你的上传库文件名即可
```

如图：

![图三.png](http://oqepgj2jp.bkt.clouddn.com/cocoapods3.png)

编辑`podspec`文件(最好用代码编辑器打开进行编辑)：

```
Pod::Spec.new do |s|
  s.name         = "SJRSAEncryptor"
  s.version      = "1.0.0"
  s.summary      = "A iOS RSA Encryptor tool."
  s.description  = "A iOS RSA Encryptor tool, easy to use it."
  s.homepage     = "https://github.com/CoderSteveJones/SJRSAEncryptor.git"
  s.license      = "MIT"
  s.author             = { "SteveJones" => "benkong_ah@foxmail.com" }
  s.source       = { :git => "https://github.com/CoderSteveJones/SJRSAEncryptor.git", :tag => "#{s.version}" }
  s.source_files  = "SJRSAEncryptor/*.{h,m}"
end
```
`name:`类库的名称这里字段介绍如下：
`version:`库的版本
`summary:`就是介绍语
`homtepage:`Github上项目地址
`license:`许可证
`author:`作者
`source:`项目的https链接地址
`source_files:`要共享的代码，这里是SJRSAEncryptor下面的所有代码。
接下来执行下面的命令进行
验证：

```
pod lib lint SJRSAEncryptor.podspec   // SJRSAEncryptor改为你的上传库文件名即可
```
如图：

![图四.png](http://oqepgj2jp.bkt.clouddn.com/cocoapods4.png)


结果多种多样，如果有错，则按照提示进行改错即可。
发现了多个警告，只要不是错误就行，警告可以直接忽略（红色也提示如何忽略）：

```
pod lib lint SJRSAEncryptor.podspec --allow-warnings   // SJRSAEncryptor改为你的上传库文件名即可
```

如图：


![图五.png](http://oqepgj2jp.bkt.clouddn.com/cocoapods5.png)

当看到`SJRSAEncryptor passed validation.`之后，就说明验证通过了。

##### 3 在Github上创建release版本
打开项目的目录，然后创建`release`版本的类库：


![图六.png](http://oqepgj2jp.bkt.clouddn.com/cocoapods6.png)

点击`release`,添加发布版本（我这已经发步过一次，所以显示1）。


![图七.png](http://oqepgj2jp.bkt.clouddn.com/cocoapods7.png)

##### 4 注册CocoaPods账号
执行命令行：

```
pod trunk register 邮箱地址  '用户名' --description='描述信息'

```

发送了一个验证码到邮箱，你可以打开你的邮箱验证即可。打开邮件中的链接后如下：

![图八.png](http://oqepgj2jp.bkt.clouddn.com/cocoapods8.png)

这样就成功注册了Cocoapods账号。
可以用
```
pod trunk me
```
检查是否创建成功。成功的结果如下：

![图九.png](http://oqepgj2jp.bkt.clouddn.com/cocoapods9.png)


然后执行：

```
pod trunk push SJRSAEncryptor.podspec --allow-warnings   // SJRSAEncryptor改为你的上传库文件名即可
```

执行结果如下：


![图十.png](http://oqepgj2jp.bkt.clouddn.com/cocoapods10.png)


说明了已经上传成功。


##### 6 检查上传是否成功

```
pod search SJRSAEncryptor
```



#### 四、参考文档：
[http://www.cnblogs.com/zhanggui/p/6003481.html](http://www.cnblogs.com/zhanggui/p/6003481.html)
[http://www.cocoachina.com/ios/20160415/15939.html](http://www.cocoachina.com/ios/20160415/15939.html)
[http://www.cocoachina.com/ios/20160907/17501.html](http://www.cocoachina.com/ios/20160907/17501.html)
[https://cocoapods.org/](https://cocoapods.org/)

