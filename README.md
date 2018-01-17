# water

vue2 + webapp

# 安装依赖

 >npm install

# 测试

 >node config/dev-server.js

# 打包

 >npm run build

# 技术栈

  + 1 vue2  核心
  + 2 vue-router 路由
  + 3 vuex 管理状态
  + 4 vue-resource ajax获取数据
  + 5 vue-amazeui 界面框架
  + 6 http://vue.ydui.org 使用部分组件做界面框架

# 开发前准备，请自行百度
  + 1 安装 node.js
  + 2 安装 cnpm
  + 3 vs code 开发工具
  + 4 github 桌面版

# 开发日志

### _2018-1-2 至 2018-1-5_ 

 + 1 搭建框架、梳理引用 √
 + 2 设计目录、页面关系 √

### _2018-1-8 至 2018-1-12_

 + 1 调整首页+三条红线的样式 √
 + 2 完成地图模块跟数据的联动 √
 + 3 完成查询组件的事件切换 √
 + 4 搭建condova环境 × -- 暂时不考虑这种方式

### _2018-1-15 至 2018-1-19_

 + 1 图片上传组件 √
 + 2 图片切换组件 √
 + 3 搜索组件 √
 + 4 接口开发准备 --other
 + 5 下拉加载组件 √
 + 6 地图上的定位 
 + 7 页面权限思考 
 + 8 打包后在各款安卓机器上 全面测试 

# 目录
 
+ --config
+   ----dev-server.js 开发测试
+ --src
+   ----components vue 组件
+   ----libs 第三方的 js 依赖
+   ----store 
+     --- api 接口的前缀
+     --- modules 每个页面的实际动作
+   ----views 每个功能页面
+   ----main.js 路由规则及全局变量的注入
+ --statics 自己的css 或 下载css
+   ---- css 
+   ---- images
+   ---- fonts
+ ----index.html 用于注入的index模板
+ ----package.json 依赖信息
+ ----webpack.config.js 打包信息

# 待研究的内容
  + 1 拍照上传 （已完成）
  + 2 app 增量打包


# 页面详细说明

### _App.vue_
      所有切换的路由都在这里展示

### _HomeView.vue_
      首页由组件 headbar 
### _RedView.vue_
      红线由组件 headbar ,doufu
### _RedView-v1.vue_
      三条红线，新的界面样式
### _RouteView.vue_    
      巡查页面
### _CheckView.vue_    
      考核管理页面

### _RedView-water.vue_
      子页面,取水总量
### _RedView-query.vue_    
      子页面，查询和列表 
### _RedView-qsh-details.vue_    
      子页面，取水户详情页面 
### _RouteView-plan.vue_    
      子页面，巡检计划
### _RouteView-alert.vue_    
      子页面，报警站点
### _RouteView-reback-details.vue_          
      子页面，巡检反馈

### _searchbar.vue_
      头部搜索组件
### _headback.vue_
      带回退的组件，带标题
### _doufu.vue_
      豆腐块组件
### _topquery.vue_
      下拉式弹出查询组件
### _redlists.vue_
      红线列表组件
### _routelists.vue_
      巡查列表组件
### _redmap.vue_
      地图组件


# 组件BUG待解决
  + 1 tabbar在active和href并存的时候，有切换失灵的情况出现
  + 2 vue-amazeui 样式不全满足，需要重新发布一个自己的