title: AngularJS小结
date: 2016-03-30 16:55:00
categories:
tags: [angularJS]
---

### 1.去掉AngularJS路由的＃

        $locationProvider.html5Mode(true);
        //or
        $locationProvider.html5Mode({
            enabled: true,
            requireBase: false
          });
### 2.指令不可平行（V1.3.2）
多个指令不能这样排列引用，结果是只能读取到第一个“directive-one”

        <div>
            <directive-one/>
            <directive-two/>
            <directive-three/>
        </div>
解决办法：

        1）<div directive-one></div>（推荐）
        2）<div>  <directive-one/>  </div> 

### 3.变量名和模块名最好不要同名；指令模版里不能有与指令同名的类名（报错：$compile:multidir） 
### 4.$scope绑定失效
首先你当然要检查有没有错误以及是否确实是scope变量，如果这些都没问题，那么多半儿是 $apply  导致的。对于大多数操作，$apply都会自动执行，所以你不用担心，但是如果你使用了angular之外的功能，比如直接调用了setTimeout函数、挂接了jquery的事件、使用了jquery的ajax操作等等，那么系统就没有机会帮你调用$apply，界面也就没有机会刷新了，但是你如果之后又做了其他会导致$apply的操作，你会发现以前“欠下”的那次界面刷新被正常执行了了 …… 迟到的刷新仍然是bug。
### 5.ng-if影响ng-module双向绑定
原因：ng-if会创建一个新的child $scope  
解决方法：

        <input ng-module="$parent.username" />
### 6.angular.module的两种写法
angular.module('app', []); 创建一个名为app的模块，且不依赖其他任何模块，如果已经有了一个同名模块，则会覆盖现有的。
angular.module('app'); 是查找一个现有module，如果这个module不存在，则返回空值。
### 7.ng-show与ng-if的区别
ng-show: DOM元素存在，但不显示
ng-if: DOM元素需重新渲染，会创建新的子 $scope
### 8.项目的文件结构
在项目中有条理的组织文件结构是必要的，对angular项目而言一般有这两种思路：按类型、按功能
按类型：

        controllers/
            LoginController.js
            RegistrationController.js
            ProductDetailController.js
            SearchResultsController.js
        directives.js
        filters.js
        models/
            CartModel.js
            ProductModel.js
            SearchResultsModel.js
            UserModel.js
        services/
            CartService.js
            UserService.js
            ProductService.js

按功能模块：

        cart/
            CartModel.js
            CartService.js
        common/
            directives.js
            filters.js
        product/
        search/
            SearchResultsController.js
            SearchResultsModel.js
            ProductDetailController.js
            ProductModel.js
            ProductService.js
        user/
            LoginController.js
            RegistrationController.js
            UserModel.js
            UserService.js

### 9. $apply $digest
 $apply会使ng进入$digest cycle, 并从$rootScope开始遍历(深度优先)检查数据变更。
 $digest仅会检查该scope和它的子scope，当你确定当前操作仅影响它们时，用$digest可以稍微提升性能。$digest是在AngularJS进行脏数据检查时调用的（脏数据并不是废弃和无用的数据，而是状态前后发生变化的数据）
### 10.延迟执行
一些不必要的操作，放到$timeout里面延迟执行。
如果不涉及数据变更，还可以加上第三个参数false，避免调用$apply。
对时间有要求的，第二个参数可以设置为0。

        $http.get('http://path/to/url').success(function(data){
          $scope.name = data.name;
          $timeout(function(){
            //do sth later, such as log
          }, 0, false);
        });
### 11.$evalAsync vs $timeout
[http://stackoverflow.com/questions/17301572/angularjs-evalasync-vs-timeout](http://stackoverflow.com/questions/17301572/angularjs-evalasync-vs-timeout)
directive中执行的$evalAsync， 会在angular操作DOM之后，浏览器渲染之前执行。
controller中执行的$evalAsync， 会在angular操作DOM之前执行，一般不这么用。
而使用$timeout，会在浏览器渲染之后执行。

### 12.优化ng-repeat
1)限制列表个数
    列表对象的数据转换，在放入scope之前处理。如$scope.dataList = convert(dataFromServer)
    可以使用ngInfiniteScroll来做无限滚动。
2）使用track by
    刷新数据时，我们常这么做：$scope.tasks = data || [];，这会导致angular移除掉所有的DOM，重新创建和渲染。
    若优化为ng-repeat="task in tasks track by task.id后，angular就能复用task对应的原DOM进行更新，减少不必要渲染。
    [http://www.codelord.net/2014/04/15/improving-ng-repeat-performance-with-track-by](http://www.codelord.net/2014/04/15/improving-ng-repeat-performance-with-track-by)

_$digest $apply $watch $http $location $timeout $interval_
