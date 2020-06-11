# Vue项目化

## 前言：

《vue.js从入门到项目实战》的第六章和第八章。尝试一下Vue项目化的过程。

前置内容：[vue的基础知识](https://blog.csdn.net/weixin_42875245/article/details/106558173)

上次学习了《vue.js从入门到项目实战》的前六章，重点学习了第二、三、四章的Vue实例和模板语法；了解了一下Vue组件（可复用的Vue实例）和Vue项目化（Vue CLI、Vue router、vuex）

接触了一部分Vue项目化的理论，这次对这一部分进行实践，边实践边记录遇到的问题。

[toc]

## 理论内容

### Vue脚手架：Vue CLI

是Vue官方提供的构建工具，五分钟就可以搭建一个完整的Vue应用。



### 前端路由：Vue router

ajax实现了无刷新的数据交互、前端路由实现了无刷新的页面跳转。ajax将web page发展成web app，而前端路由给web app增加了更多可能，如单页面应用。

Vue router是官方提供的路由管理器，致力于简化单页面应用的构建。

### 状态管理：Vuex

对于小型应用来说，完全没必要引入状态管理，因为这会带来更多开发成本。但是当应用复杂度越来越高，状态管理也越发重要起来。

官网提供的状态管理器为vuex，用于管理分散在Vue各个组件中的数据。

## 遇到的问题

npm的使用我是参照《vue.js从入门到项目实战》的第二章（1-3）和第六章（4-6）进行操作的。

### 1npm安装淘宝镜像报错

输入

```
npm install -g cnpm --registry=https://registry.npm.taobao.org
```

输出

```
npm should be run outside of the node repl, in your normal shell.
(Press Control-D to exit.)
```

这个报错的意思是npm应该在node repl之外的正常shell中运行。（按Control-D退出。）

然后我复制这个报错信息进行搜索。

[如何解决npm should be run outside of the node repl, in your normal shell问题](https://blog.csdn.net/hwhsong/article/details/51900990)

里面解释是npm不能在node开发模式中运行npm等命令，只能在cmd中才能运行。

因为我之前曾用cmd启动过mysql，于是照葫芦画瓢操作一下，发现还真行。完美。

```
//输入cd..表示返回上一层文件夹；
C:\Users\Administrator>cd..

C:\Users>cd..
//输入cd [地址]表示进入地址所在文件夹
C:\>cd C:\Program Files\nodejs
//最后我尝试安装淘宝镜像，还想还真行。
C:\Program Files\nodejs>npm install -g cnpm --registry=https://registry.npm.taobao.org
C:\Users\Administrator\AppData\Roaming\npm\cnpm -> C:\Users\Administrator\AppData\Roaming\npm\node_modules\cnpm\bin\cnpm
+ cnpm@6.1.1
added 685 packages from 957 contributors in 40.672s

C:\Program Files\nodejs>
```

好奇之下，我看了看淘宝镜像，发现这小可爱藏到了隐藏目录AppDate文件夹中。

### 2安装vue.js报错

输入：

cnpm install vue

输出：

```
× Install fail! Error: EPERM: operation not permitted, mkdir 'C:\Program Files\nodejs\node_modules\_vue@2.6.11@vue'
Error: EPERM: operation not permitted, mkdir 'C:\Program Files\nodejs\node_modules\_vue@2.6.11@vue'
npminstall version: 3.27.0
npminstall args: C:\Program Files\nodejs\node.exe C:\Users\Administrator\AppData\Roaming\npm\node_modules\cnpm\node_modules\npminstall\bin\install.js --fix-bug-versions --china --userconfig=C:\Users\Administrator\.cnpmrc --disturl=https://npm.taobao.org/mirrors/node --registry=https://r.npm.taobao.org vue
```

经过我的仔细观察，我发现操作介绍是说cnpm安装，而不是npm安装，于是猜想是要用cnpm的路径进行操作；于是操作一波，发现成功了。果然知识都是触类旁通的。

```
C:\Program Files\nodejs>cd..

C:\Program Files>cd..

C:\>cd C:\Users\Administrator\AppData\Roaming\npm\node_modules\cnpm\bin

C:\Users\Administrator\AppData\Roaming\npm\node_modules\cnpm\bin>cnpm install vue
√ Installed 1 packages
√ Linked 0 latest versions
√ Run 0 scripts
√ All packages installed (1 packages installed from npm registry, used 2s(network 2s), speed 488.85kB/s, json 1(27.82kB), tarball 825.22kB)

C:\Users\Administrator\AppData\Roaming\npm\node_modules\cnpm\bin>
```

### 3引入Vue模块报错

输入：

```
C:\Users\Administrator\AppData\Roaming\npm\node_modules\cnpm\bin>import Vue from 'vue'
```

输出：

```
'import' 不是内部或外部命令，也不是可运行的程序
或批处理文件。
```

然后我思考了一下，这应该和我用cmd来操作有关，我使用的命令应该只能是那个文件夹内的命令。而那个文件夹没有import命令。

这个import命令应该是在main.js中引入。而不是在这个控制台使用。

### 4安装Vue CLI没报错

```
C:\Users\Administrator\AppData\Roaming\npm\node_modules\cnpm\bin>cnpm install vue-cli -g
Downloading vue-cli to C:\Users\Administrator\AppData\Roaming\npm\node_modules\vue-cli_tmp
Copying C:\Users\Administrator\AppData\Roaming\npm\node_modules\vue-cli_tmp\_vue-cli@2.9.6@vue-cli to C:\Users\Administrator\AppData\Roaming\npm\node_modules\vue-cli
Installing vue-cli's dependencies to C:\Users\Administrator\AppData\Roaming\npm\node_modules\vue-cli/node_modules
[1/20] commander@^2.9.0 installed at node_modules\_commander@2.20.3@commander
[2/20] consolidate@^0.14.0 installed at node_modules\_consolidate@0.14.5@consolidate
[3/20] minimatch@^3.0.0 installed at node_modules\_minimatch@3.0.4@minimatch
[4/20] ora@^1.3.0 installed at node_modules\_ora@1.4.0@ora
[5/20] rimraf@^2.5.0 existed at node_modules\_rimraf@2.7.1@rimraf
[6/20] multimatch@^2.1.0 installed at node_modules\_multimatch@2.1.0@multimatch
[7/20] handlebars@^4.0.5 installed at node_modules\_handlebars@4.7.6@handlebars
[8/20] semver@^5.1.0 installed at node_modules\_semver@5.7.1@semver
[9/20] chalk@^2.1.0 installed at node_modules\_chalk@2.4.2@chalk
[10/20] read-metadata@^1.0.0 installed at node_modules\_read-metadata@1.0.0@read-metadata
[11/20] uid@0.0.2 installed at node_modules\_uid@0.0.2@uid
[12/20] coffee-script@1.12.7 existed at node_modules\_coffee-script@1.12.7@coffee-script
[13/20] tildify@^1.2.0 installed at node_modules\_tildify@1.2.0@tildify
[14/20] user-home@^2.0.0 installed at node_modules\_user-home@2.0.0@user-home
[15/20] validate-npm-package-name@^3.0.0 installed at node_modules\_validate-npm-package-name@3.0.0@validate-npm-package-name
[16/20] metalsmith@^2.1.0 installed at node_modules\_metalsmith@2.3.0@metalsmith
[17/20] async@^2.4.0 installed at node_modules\_async@2.6.3@async
[18/20] download-git-repo@^1.0.1 installed at node_modules\_download-git-repo@1.1.0@download-git-repo
[19/20] request@^2.67.0 installed at node_modules\_request@2.88.2@request
[20/20] inquirer@^6.0.0 installed at node_modules\_inquirer@6.5.2@inquirer
deprecate metalsmith@2.3.0 › gray-matter@2.1.1 › coffee-script@^1.12.4 CoffeeScript on NPM has moved to "coffeescript" (no hyphen)
Recently updated (since 2020-06-04): 1 packages (detail see file C:\Users\Administrator\AppData\Roaming\npm\node_modules\vue-cli\node_modules\.recently_updates.txt)
  2020-06-08
    → request@2.88.2 › har-validator@5.1.3 › ajv@6.12.2 › fast-deep-equal@^3.1.1(3.1.3) (15:27:28)
All packages installed (235 packages installed from npm registry, used 8s(network 7s), speed 689.39kB/s, json 221(458.22kB), tarball 4.56MB)
[vue-cli@2.9.6] link C:\Users\Administrator\AppData\Roaming\npm\vue@ -> C:\Users\Administrator\AppData\Roaming\npm\node_modules\vue-cli\bin\vue
[vue-cli@2.9.6] link C:\Users\Administrator\AppData\Roaming\npm\vue-init@ -> C:\Users\Administrator\AppData\Roaming\npm\node_modules\vue-cli\bin\vue-init
[vue-cli@2.9.6] link C:\Users\Administrator\AppData\Roaming\npm\vue-list@ -> C:\Users\Administrator\AppData\Roaming\npm\node_modules\vue-cli\bin\vue-list

C:\Users\Administrator\AppData\Roaming\npm\node_modules\cnpm\bin>vue --version
2.9.6
```

### 5初始化项目出现了一个有意思的事

输入vue init webpack my-project后，需要enter才能继续操作，知道enter完后才是初始化。

仔细看题，发现这原来是Vue CLI引导的项目配置。

然后对比作者的项目配置，发现我和作者最后三步不同，作者选择No。然后他就没这么多下载的步骤直接to get started:。

作者给出的解释是“Set up unit tests”和“Setup e2e tests with Nightwatch”选择“No”，这部分内容和Vue没有直接关系。

最后一项选择No是因为npm的镜像源在国外，安装依赖的速度缓慢且容易出错，故选择cnpm安装。

```
? Project name my-project
? Project description A Vue.js project
? Author wsdchong <wsdchong@outlook.com>
? Vue build standalone
? Install vue-router? Yes
? Use ESLint to lint your code? Yes
? Pick an ESLint preset Standard
? Set up unit tests Yes
? Pick a test runner jest
? Setup e2e tests with Nightwatch? Yes
? Should we run `npm install` for you after the project has been created? (recommended) npm

   vue-cli · Generated "my-project".


# Installing project dependencies ...
# ========================

npm WARN deprecated extract-text-webpack-plugin@3.0.2: Deprecated. Please use https://github.com/webpack-contrib/mini-css-extract-plugin
npm WARN deprecated browserslist@2.11.3: Browserslist 2 could fail on reading Browserslist >3.0 config used in other tools.
npm WARN deprecated request@2.88.2: request has been deprecated, see https://github.com/request/request/issues/3142
npm WARN deprecated core-js@2.6.11: core-js@<3 is no longer maintained and not recommended for usage due to the number of issues. Please, upgrade your dependencies to the actual version of core-js@3.
npm WARN deprecated bfj-node4@5.3.1: Switch to the `bfj` package for fixes and new features!
npm WARN deprecated chokidar@2.1.8: Chokidar 2 will break on node v14+. Upgrade to chokidar 3 with 15x less dependencies.
npm WARN deprecated mkdirp@0.5.1: Legacy versions of mkdirp are no longer supported. Please update to mkdirp 1.x. (Note that the API surface has changed to use Promises in 1.x.)
npm WARN deprecated json3@3.3.2: Please use the native JSON object instead of JSON 3
npm WARN deprecated fsevents@1.2.13: fsevents 1 will break on node v14+ and could be using insecure binaries. Upgrade to fsevents 2.
npm WARN deprecated browserslist@1.7.7: Browserslist 2 could fail on reading Browserslist >3.0 config used in other tools.
npm WARN deprecated circular-json@0.3.3: CircularJSON is in maintenance only, flatted is its successor.
npm WARN deprecated socks@1.1.10: If using 2.x branch, please upgrade to at least 2.1.6 to avoid a serious bug with socket data flow and an import issue introduced in 2.1.0
npm WARN deprecated left-pad@1.3.0: use String.prototype.padStart()
npm WARN deprecated resolve-url@0.2.1: https://github.com/lydell/resolve-url#deprecated
npm WARN deprecated urix@0.1.0: Please see https://github.com/lydell/urix#deprecated

> chromedriver@2.46.0 install C:\Users\Administrator\AppData\Roaming\npm\node_modules\cnpm\bin\my-project\node_modules\chromedriver
> node install.js

Current existing ChromeDriver binary is unavailable, proceding with download and extraction.
Downloading from file:  https://chromedriver.storage.googleapis.com/2.46/chromedriver_win32.zip
Saving to file: C:\Users\ADMINI~1\AppData\Local\Temp\2.46\chromedriver\chromedriver_win32.zip
Received 781K...
Received 1566K...
Received 2350K...
Received 3134K...
Received 3918K...
Received 4523K total.
Extracting zip contents
Copying to target path C:\Users\Administrator\AppData\Roaming\npm\node_modules\cnpm\bin\my-project\node_modules\chromedriver\lib\chromedriver
Done. ChromeDriver binary available at C:\Users\Administrator\AppData\Roaming\npm\node_modules\cnpm\bin\my-project\node_modules\chromedriver\lib\chromedriver\chromedriver.exe

> core-js@2.6.11 postinstall C:\Users\Administrator\AppData\Roaming\npm\node_modules\cnpm\bin\my-project\node_modules\core-js
> node -e "try{require('./postinstall')}catch(e){}"

Thank you for using core-js ( https://github.com/zloirock/core-js ) for polyfilling JavaScript standard library!

The project needs your help! Please consider supporting of core-js on Open Collective or Patreon:
> https://opencollective.com/core-js
> https://www.patreon.com/zloirock

Also, the author of core-js ( https://github.com/zloirock ) is looking for a good job -)


> uglifyjs-webpack-plugin@0.4.6 postinstall C:\Users\Administrator\AppData\Roaming\npm\node_modules\cnpm\bin\my-project\node_modules\webpack\node_modules\uglifyjs-webpack-plugin
> node lib/post_install.js

npm notice created a lockfile as package-lock.json. You should commit this file.
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: fsevents@^1.2.3 (node_modules\sane\node_modules\fsevents):
npm WARN notsup SKIPPING OPTIONAL DEPENDENCY: Unsupported platform for fsevents@1.2.13: wanted {"os":"darwin","arch":"any"} (current: {"os":"win32","arch":"x64"})
npm WARN notsup Unsupported engine for watchpack-chokidar2@2.0.0: wanted: {"node":"<8.10.0"} (current: {"node":"14.0.0","npm":"6.14.4"})
npm WARN notsup Not compatible with your version of node/npm: watchpack-chokidar2@2.0.0
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: fsevents@~2.1.2 (node_modules\chokidar\node_modules\fsevents):
npm WARN notsup SKIPPING OPTIONAL DEPENDENCY: Unsupported platform for fsevents@2.1.3: wanted {"os":"darwin","arch":"any"} (current: {"os":"win32","arch":"x64"})
npm WARN ajv-keywords@2.1.1 requires a peer of ajv@^5.0.0 but none is installed. You must install peer dependencies yourself.

added 1822 packages from 1110 contributors and audited 1830 packages in 91.672s

30 packages are looking for funding
  run `npm fund` for details

found 99 vulnerabilities (76 low, 9 moderate, 13 high, 1 critical)
  run `npm audit fix` to fix them, or `npm audit` for details


Running eslint --fix to comply with chosen preset rules...
# ========================


> my-project@1.0.0 lint C:\Users\Administrator\AppData\Roaming\npm\node_modules\cnpm\bin\my-project
> eslint --ext .js,.vue src test/unit test/e2e/specs "--fix"


# Project initialization finished!
# ========================

To get started:

  cd my-project
  npm run dev

Documentation can be found at https://vuejs-templates.github.io/webpack
```

### 6安装项目依赖出现问题

```
C:\Users\Administrator\AppData\Roaming\npm\node_modules\cnpm\bin>cnpm install
C:\Users\Administrator\AppData\Roaming\npm\node_modules\cnpm\bin>ppData\Roaming\npm\node_modules\cnpm\bin\package.json
```

果然被第5步说中了，安装依赖容易出错，bin文件夹中没有package.json。

```
√ Installed 0 packages
√ Linked 0 latest versions
√ Run 0 scripts
√ All packages installed (used 20ms(network 6ms), speed 0B/s, json 0(0B), tarball 0B)
```

怎么办呢。那再一次初始化一次项目。最后三步按照作者的操作来操作。

```
npminstall WARN package.json not exists: C:\Users\Administrator\AppData\Roaming\npm\node_modules\cnpm\bin\package.json
√ Installed 0 packages
√ Linked 0 latest versions
√ Run 0 scripts
√ All packages installed (used 15ms(network 7ms), speed 0B/s, json 0(0B), tarball 0B)
```

结果bin文件夹就是没有package.json。

于是我猜测应该是需要我进入到my-project中，然后进行cnpm install和npm start；

果然成功了。

```
 DONE  Compiled successfully in 7505ms                                                                      下午9:41:41

 I  Your application is running here: http://localhost:8080
```

## 尝试运行第八章的项目

首先Ctrl+C进行终止批处理操作；

然后返回my-project的上一级文件夹；

最后把第八章的项目拷贝到bin文件夹；

```
 I  Your application is running here: http://localhost:8080
终止批处理操作吗(Y/N)?
终止批处理操作吗(Y/N)? y

C:\Users\Administrator\AppData\Roaming\npm\node_modules\cnpm\bin\my-project>cd..

C:\Users\Administrator\AppData\Roaming\npm\node_modules\cnpm\bin>vue init webpack chapter07

? Target directory exists. Continue? Yes
? Project name chapter07
? Project description A Vue.js project
? Author wsdchong <wsdchong@outlook.com>
? Vue build standalone
? Install vue-router? Yes
? Use ESLint to lint your code? Yes
? Pick an ESLint preset Standard
? Set up unit tests No
? Setup e2e tests with Nightwatch? No
? Should we run `npm install` for you after the project has been created? (recommended) no

   vue-cli · Generated "chapter07".

# Project initialization finished!
# ========================

To get started:

  cd chapter07
  npm install (or if using yarn: yarn)
  npm run lint -- --fix (or for yarn: yarn run lint --fix)
  npm run dev

Documentation can be found at https://vuejs-templates.github.io/webpack
```

然后cnpm install和npm start；

最后浏览器里看看。

居然和之前那个一样。烦。今天晚上先到这。明天再弄。