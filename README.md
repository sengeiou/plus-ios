文档编写中

<p align="center"><img src="http://oppt2zece.bkt.clouddn.com/plus.png"></p>

TS+ iOS code repository.

该工程使用 swift 3.0 语言编写.支持 iOS 9.0 以上系统.

重要说明记录在 README.md 文件.

和整个项目相关的决策工作安排等记录在[thinksns-plus-document](https://github.com/zhiyicx/thinksns-plus-document).

本工程的文档部分遵循[智艺创想文档审核标准](https://github.com/zhiyicx/mobile-devices-code-style-guide/wiki/智艺创想文档审核标准)

本工程的UI遵循[TS+ 移动端视觉规范](https://github.com/zhiyicx/thinksns-plus-document/tree/master/document/TS%2B%E8%A7%86%E8%A7%89%E8%A7%84%E8%8C%83%202.0) 2.0

注意： 需要二次开发的，请在开发分支develop分支上面进行修改，不要使用master分支直接修改，master分支将用于更新ts+最新代码，如需要新的代码，请自行将master分支代码合并到develop分支上。

**目录**

* [注意事项](#注意事项)
* [工程文件树状图说明](https://github.com/slimkit/thinksns-plus-guide/blob/master/%E6%8A%80%E6%9C%AF%E6%96%87%E6%A1%A3/iOS%E7%AB%AF/Thinksns%20Plus%20Document/%E5%B7%A5%E7%A8%8B%E6%96%87%E4%BB%B6%E7%BB%93%E6%9E%84%E8%AF%B4%E6%98%8E.md)
    * [图片文件夹树状图说明](#图片文件夹树状图说明)
* [文档说明](#文档说明)
    * [详细说明文档目录](#详细说明文档目录)
    * [文档更新时间规则](#文档更新时间规则)
* [分支使用说明](#分支使用说明)
    * [分支关系](#分支关系)
* [统一缩写备注表](#统一缩写备注表)
* [开发工具](#开发工具)

## 注意事项

1. 本工程日志输出信息必须使用`LogCenter`输出,错误信息统一使用`TSErrorCenter`内记录的错误信息.**不允许**自定义日志输出和错误信息.
2. 为了方便后续使用自动化工具筛检`commit`内容,规定每次提交和`issues`相关的代码时,使用统一格式: 在提交信息末尾空一格,空一格后记录下`commit`类型,然后再在英文符号的括号内填写`issues code`.默认的 commit 类型为: 代码,文档以及测试

    示例代码:```(#9527) 文档 提交信息```
    示例代码:```(#1 #2  #3) 测试 提交信息```
 
3. 本工程统一使用 `SwiftLint`工具检查代码风格.
    * `SwiftLint`检查规则记录在`./.swiftLint.yml`文件内.
    * 安装方法: 双击根目录下的`SwiftLint.pkg`
    * 使用方法,每次构建工程`(commend + B)`不满足代码风格的代码会通过`Xcode`提示警告和错误.
    * `Thinksns Plus/Libraries/`文件夹下的文件不会进行代码风格检测.
4. 本工程统一使用`TSReachability`检测网络状态.
5. 本工程所有的图片统一添加`IMG_`前缀,从而避免在`Xcode 8`编辑器下输入代码时,不必要的提示图片自动补全.
6. 本工程忽略了`pod/`目录下所有文件,需要各自下载源码后运行`$pod install`更新各自三方库.所以不能直接需改三方库源码,避免多端同步问题.
7. 本工程不允许直接使用`UIKit`默认的控件,需要使用对应的`TSUIKit`控件.
    例如:不允许直接使用`UIButton`而应该使用`TSButton`.而后编写的某些页面的具体控件都应直接使用`TSButton`或者他的子类.
    位置: `TSUIKit`记录在`./CustomUIKit/`文件夹下
8. 本工程需要使用时间时,统一使用Date类型.当和服务器交互时,使用字符串.当和数据库交互时,使用 NSDate(后续升级数据库后使用Date类型)
9. 本工程测试在逐步移除过程中(2017年05月18日14:01:36),工程内代码不严格要求单元测试,已有单元测试在迁往工具库

## 命名规则

为了减少沟通成本,TS+ 为数模模型统一了后缀命名.

1. 服务器返回的数据隐射类命名为`TS服务器返回数据Model.swift`
2. 存入数据库的数模统一命名为`TS数据库数据Object.swift`

**注意！！**
model 用于和UI进行操作交互
object 只能用于数据库更新等和数据库相关的操作
UI 不允许直接操作 object
当某些UI操作影响了 model 且需要进行数据库操作时，正常的处理方式应该为首先修改 model ，再通过 model 提供的 saveFunction 等方法进行数据库操作，该 saveFunction 方法接收和传出的参数都是 model ，函数内部操作object
新增加的 model 类，记录到各个特性UI页面文件夹下，不再记录到网络请求文件夹内(TSNetwork/NetworkManager/networkModel)

## 工程文件树状图说明

[点击查看工程文件说明](https://github.com/slimkit/thinksns-plus-guide/blob/master/%E6%8A%80%E6%9C%AF%E6%96%87%E6%A1%A3/iOS%E7%AB%AF/Thinksns%20Plus%20Document/%E5%B7%A5%E7%A8%8B%E6%96%87%E4%BB%B6%E7%BB%93%E6%9E%84%E8%AF%B4%E6%98%8E.md)

## 文档说明

本工程文档统一记录在`Thinksns Plus/Thinksns Plus Document`内. [地址](https://github.com/slimkit/thinksns-plus-guide/tree/master/%E6%8A%80%E6%9C%AF%E6%96%87%E6%A1%A3/iOS%E7%AB%AF/Thinksns%20Plus%20Document)

### 文档更新时间规则

文档在编写过程中,文档更新时间必须记录在每个文档第一行.

开发过程的中的文档,第一行记录:`文档编写中`

编写完毕的文档,第一行记录时间:`2017年02月27日`

在后续作者修改了文档和文档相关源码后,更新文档:`2017年03月1日 文档更新`

后续在使用过程中,任何查看过该文档且查看了对应模块源码的开发人员都可以更新该时间:`2017年03月2日 文档校对`

## 分支使用说明

为了同时保证开发的同时修复和发布，以及为了减少不必要的分支导致远端仓库分支的混乱。现规定分支功能和命名方式如下：

1. 远端仓库**只允许**存在`master,develop,hot_fix,release`以及需要PR审核的分支
    * master 该分支记录稳定对外发布的版本。要求该分支上的最新节点总是稳定可打包可对外交付代码。
    * develop 该分支是 master 的子分支，该分支记录开发中的内容，同期开发人员的所有开发内容均是该分支的子分支。要求开发周期内每个工作日保证开发的代码更新到该分支。
    * hot_fix 该分支是 master 的子分支，该分支在每个版本发布后，产生的 BUG 需要**紧急修复**的代码提交的分支位于该分支上，同期修复 BUG 的修复人员的所有修复分支是该分支的子分支。要求，只有**紧急修复**的内容记录到该分支和该分支的自分支上，每个交付周期内的部分 BUG 可能会作为特性进入下一个开发周期，通过 develop 来解决，同时该分支修复的内容也会合并到 develop 分支上。
    * release 该分支是 master 和 develop 间的过度分支，develop 开发分支的内容完毕后，合并至该分支进行内测版本打包发布，稳定后合并至 master 进行存档记录打上 tag。要求，该分支上产生的问题通过 develop 分支进行修复和下次发布，hot_fix 和 该分支无交集。
2. 本地仓库存在远端分支远端分支的子分支，以及 `future` 分支
    * future 分支是 develop 的子分支，按照不同的开发功能模块进行划分。（**注意**废弃掉以前的按照不同开发人员进行特性分支的方式）

分支命名方式为`主分支名称_子分支名称_特性名称`

示例:

```shell
develop ( 主分支 )
future_login ( 功能分支 )

```

## 统一缩写备注表

| 全称 | 缩写 | 备注 |
|:----:|:----:|:----:|
| ViewControl | VC |  |
| UserExperience | UX |  |

##  开发工具

| 名称 | 类型 | 备注 |
|:----:|:----:|:----:|
| Xcode | IDE | 版本 8.0 |
| Cocoapods | 三方包管理工具 | 版本 1.2.1 |
| SourceTree | Git 界面化管理工具 |  |
