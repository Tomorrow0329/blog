title: Tool Description
date: 2016-03-25 17:13:23
categories:
tags: [project, gulp, wx]
---

# HEXO
hexo构建个人博客常用命令：
1.启动 ： hexo server
2.新建 ：hexo new "name"

hexo中遇到的问题：
1.WARN  No layout: index.html
原因：theme修改后并没有进行安装工作，导致themes文件夹中并没有对应的文件，更没有相关的index.html文件。
Debug:
1).git pull  下载新的主题
2).直接用本地已有的主题
# GULP
前端工程自动化工具
1. gulp.src()  引用要处理的源文件
2. .pipe()     要做的处理
3. .pipe(gulp.dest())   输出
4. 默认处理

         gulp.task('default', function () {
            gulp.start('sass', 'js', 'concat') // task name
         })
         
常用的插件：
1.gulp-sass
2.gulp-watch
3.gulp-load-plugins
4.gulp-webserver
5.gulp-minify-css
6.gulp-ejs
7.gulp.spritesmith
8.gulp-rename
9.gulp-jslint,,demo:

        gulp.task('jslint', function () {
            // set your js name
            return gulp.src(config.jsBasePath + fileName + '.js')
              .pipe(plugins.jslint({
                // detail: http://jslint.com/help.html
                bitwise: false,
                browser: true,
                couch: false,
                // Be sure to turn this option off before going into production.
                devel: false,
                // es6: false,
                eval: false,
                for: true,
                fudge: true,
                maxerr: 256,
                maxlen: 160,
                node: false,
                this: true,
                white: false,
                // or you can declare them in the js as /*global aaa,bbb*/
                global: [
                  'window',
                  'jQuery',
                  '$',
                  'wx'
                ]
              }));
          });

# NPM Package
1.yargs    用于获取启动参数，处理命令行参数，针对不同参数，执行不同的代码过程
yargs模块的argv对象用来读取命令行参数

        var srgv = require('yargs').alias('n', 'name').argv;
        console.log('hello', argv.n);
当然，如果用到node中， app.js 里可以这样写：

        if (app.get('env') === 'production') {
          app.set('views', path.join(__dirname, 'views/dist'));
        } else {
          app.set('views', path.join(__dirname, 'views/dev'));
        }
        
alias指定n是name的别名

2.autoprefixer 为CSS自动添加前缀，可以通过他自由的属性来自定义需要兼容的浏览器版本、是否去掉过时的前缀等。
3.nodemon  用于获取启动参数，针对不同参数，切换任务执行过程时需要(同supervisor)
4.imagemin-pngquant  png图片压缩（gulp也有类似的工具 gulp-imagemin）

# 项目笔记
### 1.下拉列表
方法1: JS或JQ实现下拉列表效果
方法2: CSS3的transition实现相应的动画效果，无需JS啦～

        .nav-list:hover>a>.demoHeader-describe {
            height: auto;
          };
        
          .nav-list:hover .demoHeader-describe>span {
            height: 90px;
          }
        
          .demoHeader-describe {
            /*...*/
        
            transition: height 0.4s;
            -moz-transition: height 0.4s; /* Firefox 4 */
            -webkit-transition: height 0.4s; /* Safari and Chrome */
            -o-transition: height 0.4s; /* Opera */
        
            span {
              /*...*/
        
              transition: height 0.4s;
              -moz-transition: height 0.4s; /* Firefox 4 */
              -webkit-transition: height 0.4s; /* Safari and Chrome */
              -o-transition: height 0.4s; /* Opera */
            }
          }
          
### 2.gulp 工程构建
        var gulp = require ('gulp'),
          config = require('./gulp/config')(),
        
          sass = require('gulp-sass'),
          ejs = require('gulp-ejs'),
          plugins = require('gulp-load-plugins'),
          spritesmith=require('gulp.spritesmith'),
          minifycss = require('gulp-minify-css'),
          rename = require('gulp-rename'),
          imagemin = require('gulp-imagemin'),
        
          gulpTaskList = require('fs').readdirSync('./gulp/tasks');//Require some files from folder
        
        gulpTaskList.forEach(function (taskFile) {
          require('./gulp/tasks/' + taskFile)(gulp, sass, ejs, config, plugins, spritesmith, minifycss, rename, imagemin);
        });
利用gulp构建前端部分，实现前端工程化，简单实例；

### 3.微信

        wxInit = function () {
                var wxConfig = function () {
                    $.get(main.publicUrlPrefix + 'wx/js_ticket_package', {url: window.location.href}).done(function (res) {
                        wx.config({
                            debug: false,
                            appId: res.appId,
                            timestamp: res.timestamp,
                            nonceStr: res.nonceStr,
                            signature: res.signature,
                            jsApiList: [
                                'checkJsApi',
                                'chooseImage',
                                'uploadImage',
                                'onMenuShareTimeline',
                                'onMenuShareAppMessage'
                            ]
                        });
                    });
                };
                wxConfig();
                wx.ready(function () {
                    $uploadBtn.tap(function () {
                        /*...*/
                        } else {
                            $.ajax({
                                async: false,//同步
                                type: 'get',
                                url:  'test-url', //wx
                                data: {
                                    'data' : data
                                },
                                contentType: false,
                                dataType: 'json',
                                timeout: 15000,
                                success: function (res) {
                                    if (res.result) {
                                    
                                        college_id = res.college_id;
                                        
                                        wx.chooseImage({
                                            count: 1, // 默认9
                                            sizeType: ['compressed'], // 可以指定是原图还是压缩图，默认二者都有
                                            sourceType: ['album', 'camera'], // 可以指定来源是相册还是相机，默认二者都有
                                                var localId = res.localIds[0]; // 返回选定照片的本地ID列表，localId可以作为img标签的src属性显示图片
                                                loadingShow();
                                                wx.uploadImage({
                                                    localId: localId,
                                                    isShowProgressTips: 0,
                                                    success: function (res) {
                                                        var serverId = res.serverId;
                                                        $.ajax({
                                                            type: 'post',
                                                            url: 'test-url2',
                                                            data: {
                                                                'data' : data
                                                            },
                                                            dataType: 'json',
                                                            timeout: 3000,
                                                            cache: false,
                                                            success: function (res) {
                                                                /*...*/
                                                            },
                                                            error: function (res) {
                                                                // alert(JSON.stringify(data));
                                                                // alert(JSON.stringify(res));
                                                                // alert(res.status);
        
                                                                /*...*/
                                                            }
                                                        });
                                                    }
                                                });
                                            }
                                        });
                                    } else {
                                        /*...*/
                                    }
                                },
                                error: function (res) {
                                    /*...*/
                                }
                            });
                        }
                    });
                });
            };
### 4.多语言(angular-translate)
[angular-translate Doc](http://angular-translate.github.io/docs/zh-cn/#/guide)
安装、引入、基本用法

        $ bower install angular-translate
        
        //将它嵌入在自己的HTML文档中
        <script src="path/to/angular-translate.js"></script>
        
        //将angular-translate模块作为依赖注入到应用程序中
        var app = angular.module('myApp', ['pascalprecht.translate']);
        
         //应用
         app.config(['$translateProvider', function ($translateProvider) {
           $translateProvider.translations('en', {
             'TITLE': 'Hello',
             'FOO': 'This is a paragraph'
           });
          
           $translateProvider.translations('de', {
             'TITLE': 'Hallo',
             'FOO': 'Dies ist ein Absatz'
           });
          
           $translateProvider.preferredLanguage('en');
         }]);
         
          //页面
          <h1>{{ 'TITLE' | translate }}</h1>
          <p>{{ 'FOO' | translate }}</p>
