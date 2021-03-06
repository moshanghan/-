node_modules 文件夹内的内容很多，体量很大，如果使用 cnpm 安装，会更多更大，有时候出现了一些莫名其妙的错误要将 node_modules 删除，重新下载，用键盘的 delete 的自然可以删除，不过会很慢，很卡，电脑配置低一些，或者安装的包多一些，可能会导致编辑器闪退，卡死，

### 快捷除文件夹，尤其是 node_modules

```javascript
npm install rimraf -g
rimraf node_modules
```

rimraf  包的作用：以包的形式包装 rm -rf 命令，用来删除文件和文件夹的，不管文件夹是否为空，都可删除，rm -rf？自然使用此方法也可以删除

### npm 的 semver(语义化的版本控制）

[![](https://www.qdtalk.com/wp-content/uploads/2018/09/WX20180927-232621@2x.png)](https://www.qdtalk.com/wp-content/uploads/2018/09/WX20180927-232621@2x.png)  
semver 设计的初衷在于允许依赖的版本是动态的，因而可以快捷地获取到一定范围内的最新版本。下面列出了 semver 的各种形式来让我们直观地理解一下：

版本号为 a.b.c 的形式，其中 a 是大版本号，b 是小版本号，c 是补丁号。

- ^version：对应所有小版本号和补丁号。比如  ^1.0.1  可以理解为所有形式为  1.x.x 的最新版本。
- version：对应特定版本。比如版本号为  1.0.1 ，则安装的模块版本只能为  1.0.1。

动态版本使得开发者无需更改 pakcage.json 中的依赖版本信息，便可以获取到他所定义的范围内最新的版本。比如当我们通过  npm install jspdf  安装了这个包之后，package.json 中它的版本号为  ^1.3.5。当 split 这个包的作者发布了一个新的版本 1.3.6 的时候，我们下次重新执行  npm install 就会装这个 1.3.6 的版本了。

semver 带来的优势是可以使 npm 包的发布者很方便地补丁推送到使用者。比如当有一些小的 补丁 时候，用户不需要有任何感知，便可以将其中的问题修复。其实 npm 对于各个版本号的意义也有约定。

- 补丁版本发布（如 1.0.1 -> 1.0.2）：bugfix 以及微小的改动
- 小版本发布（如 1.0.1 -> 1.1.0）：添加了新的特性，同时并不会破坏原有的功能或更改接口
- 大版本发布（如 1.0.1 -> 2.0.0）：添加了破坏性的改动，有功能或接口不再兼容

npm 允许使用特殊符号，指定所要使用的版本范围，假定当前版本是 1.0.4
- 只接受补丁包：1.0 或者 1.0.x 或者 ~1.0.4
- 只接受小版本和补丁包：1 或者 1.x 或者 ^1.0.4
- 接受所有更新：\* or x

```javascript
~2.2.1 // 接受2.2.1，不接受2.3.0
^2.2.1 // 接受2.2.1和2.3.0

~2.2 // 接受2.2.0和2.2.1，不接受2.3.0
^2.2 // 接受2.2.0、2.2.1和2.3.0

~2 // 接受2.0.0、2.1.0、2.2.0、2.2.1和2.3.0
^2 // 接受2.0.0、2.1.0、2.2.0、2.2.1和2.3.0
```

还可以使用数学运算符（比如>, <, =, >= or <=等），指定版本范围

```javascript
>2.1
1.0.0 - 1.2.0
>1.0.0-alpha
>=1.0.0-rc.0 <1.0.1
^2 <2.2 || > 2.3</pre>
```

有时候也会遇到带 rc 和 beta 的

Beta：也是测试版，这个阶段的版本会一直加入新的功能。在 Alpha 版之后推出
RC：(Release 　 Candidate) 顾名思义么 ! 用在软件上就是候选版本。系统平台上就是发行候选版本。RC 版不会再加入新的功能了，主要着重于除错。
