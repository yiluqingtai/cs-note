## npm

[前端工程化（5）：你所需要的npm知识储备都在这了 (juejin.cn)](https://juejin.cn/post/6844903870578032647#heading-0)

### npm 处理 node_modules 目录结构

1、一个项目开发、上线所依赖的插件包都存放在node_modules中。虽然在实际开发中无需关注这个目录里面的文件结构细节，但了解node_modules中的内容可以帮助我们更好的理解npm组织这些文件的机制。

2、node_modules目录结构

npm 2.x 采用嵌套结构，可能会造成大量模块冗余；

npm 3.x 采用扁平结构，遇到新的包就把它安装在第一级目录，后续安装如果遇到一级目录已经存在的包，会先按照约定版本判断版本，如果符合版本约定则忽略，否则会按照npm 2.x的方式依次挂在依赖包目录下。

npm 5.x增加了package-lock.json文件，npm为了让开发者在安全的前提下使用最新的依赖包，在package.json中通常做了锁定大版本的操作，这样在每次npm install的时候都会拉取依赖包大版本下的最新的版本。这种机制最大的一个缺点就是当有依赖包有小版本更新时，可能会出现协同开发者的依赖包不一致的问题。

3、package-lock.json文件

package-lock.json文件精确描述了node_modules 目录下所有的包的树状依赖结构，每个包的版本号都是完全精确的。

package-lock.json的详细描述主要由version、resolved、integrity、dev、requires、dependencies这几个字段构成。

在开发一个应用时，建议把package-lock.json文件提交到代码版本仓库，从而让你的团队成员、运维部署人员或CI系统可以在执行npm install时安装的依赖版本都是一致的。

在开发一个库时，则不应把package-lock.json文件发布到仓库中。实际上，npm也默认不会把package-lock.json文件发布出去。之所以这么做，是因为库项目一般是被其他项目依赖的，在不写死的情况下，就可以复用主项目已经加载过的包，而一旦库依赖的是精确的版本号那么可能会造成包的冗余。

