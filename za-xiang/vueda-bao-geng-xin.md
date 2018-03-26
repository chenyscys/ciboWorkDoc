1. 首先trunk测试无误之后，先更新，保证是最新版本，再提交svn；

2. 到branch正式版上，先更新，保证正式版是最新的版本；

3. 把trunk上自己修改的文件复制到branch正式版上覆盖掉源文件，
   然后用svn的比较工具对比一下原文件，看看修改了什么内容，是否正确；

4. 确认无误后先提交，再打包。

5. 到网站branches/201801/public中，把之前的dist文件夹删除，然后把打包好的dist文件夹复制过去；

6. 更新测试，则连上29服务器执行以下几条命令： svn update svn://192.168.3.29/svn/cibohome\_v/trunk /mnt/xvdb1/www/vue/cibohome
   cd /mnt/xvdb1/www/vue/cibohome

   npm run build

   rm -rf /mnt/xvdb1/www/composer/ciboapp/public/dist

   cp -Rf dist /mnt/xvdb1/www/composer/ciboapp/public

---

最后，请前端的小伙伴再更新正式版的时候谨慎对待，严紧更新！！！



