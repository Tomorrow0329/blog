title: Tool Description
date: 2016-03-25 17:13:23
categories:
tags: [project]
---

# HEXO
hexo构建个人博客常用命令：
1.启动 ： hexo server
2.新建 ：hexo new "name"

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
6.autoprefixer
7.yargs    用于获取启动参数，针对不同参数，执行不同的代码过程
8.nodemon  用于获取启动参数，针对不同参数，切换任务执行过程时需要