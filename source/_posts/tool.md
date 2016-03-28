title: Tool Description
date: 2016-03-25 17:13:23
categories:
tags: [project]
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

# NPM Package
1.yargs    用于获取启动参数，处理命令行参数，针对不同参数，执行不同的代码过程
yargs模块的argv对象用来读取命令行参数

        var srgv = require('yargs').alias('n', 'name').argv;
        console.log('hello', argv.n);
        
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
