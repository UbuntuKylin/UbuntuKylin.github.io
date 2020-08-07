# Ubuntu Kylin Wiki
本项目为优麒麟百科，欢迎各位添加内容

## 添加规则
本wiki使用hexo框架搭建，使用githubpages发布，项目默认位于master分支。新增文章在source/_posts目录下，该目录下的文章会根据路径产生相应的分级，文章请使用markdown编写，图片请采用外链的模式。请注意:

- 请各位每次进行提交前务必先执行git pull命令，第一次将项目clone到本地时需要先安装nodejs，然后在项目目录执行npm install hexo -g，不过npm默认源在国外，推荐使用淘宝的镜像使用cnpm，具体请看官方教程：https://developer.aliyun.com/mirror/NPM。

- 每次新增文章请使用hexo new + 文章名的形式，再将其放置到相应目录。

- 各位修改请在本地执行`hexo s`来测试,确认无误后再进行提交。

- 请各位仅对hexo分支进行修改，并在每次提交前执行`hexo clean`命令。
