1. 安装TensorFlow.js的两种方式

   * html文件中直接引入script标签

   ```javascript
   <script src="https://cdn.bootcss.com/tensorflow/1.6.0/tf.min.js"></script>
   ```

   * npm安装

   ```javascript
   npm i nrm -g // 切换镜像源
   nrm ls //列出可选择的镜像源
   nrm use taobao // 选择淘宝镜像源
   
   npm i http-server -g // 安装本地服务器
   hs // 启动本地服务器
   
   npm init // 生成package.json文件
   npm i @tensorflow/tfjs // 安装tensorflow.js
   
   npm install -g parcel-bundler// 安装打包工具
   
   // 新建html文件，引入index.js文件
   // 新建index.js文件
   parcel index.html
   parcel build index.html
   
   
   // 服务器版本
   npm i windows-build-tools@4.0.0 -g
   npm i node-gyp -g
   npm i @tensorflow/tfjs-node -g
   
   npm cache clean --force // 清理缓存
   ```

