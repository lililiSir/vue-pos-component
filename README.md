# vue-pos-component
在vue-pos的基础上，将首页面上面的全部提取出来，做成单独的组件，并对组件中的方法和属性进行操作

顺便说一下，如果有的小伙伴刚开始学习使用git，在连接github的仓库时，可能会出现以下问题
git在push的时候总是出现：
fatal: remote error:  
You can't push to git://github.com/user_name/user_repo.git  
Use git@github.com:user_name/user_repo.git
解决办法
$ git remote rm origin  
$ git remote add origin git@github.com:user_name/user_repo.git  
$ git push origin

如果在git clone的时候用的是git://github.com:xx/xxx.git的形式, 那么就会出现这个问题，因为这个protocol是不支持push的

可以改成
$git clone git@github.com:username/myNCCL.git 就可以了正常的push了


# pos

> A Vue.js project

## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build

# build for production and view the bundle analyzer report
npm run build --report
```

For a detailed explanation on how things work, check out the [guide](http://vuejs-templates.github.io/webpack/) and [docs for vue-loader](http://vuejs.github.io/vue-loader).
