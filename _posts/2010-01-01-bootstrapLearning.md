---
layout: post
title: Bootstrap Learning
comments: false
keywords: Bootstrap
category: 学习
---
#轮播示例
<ul class="pagination">
  <li><a href="#">&laquo;</a></li>
  <li><a href="#">1</a></li>
  <li><a href="#">2</a></li>
  <li><a href="#">3</a></li>
  <li><a href="#">4</a></li>
  <li><a href="#">5</a></li>
  <li><a href="#">&raquo;</a></li>
</ul>

--
<nav class="navbar navbar-default" role="navigation">
   <div class="navbar-header">
      <a class="navbar-brand" href="#">W3Cschool</a>
   </div>
   <div>
      <form class="navbar-form navbar-left" role="search">
         <div class="form-group">
            <input type="text" class="form-control" placeholder="Search">
         </div>
         <button type="submit" class="btn btn-default">提交按钮</button>
      </form>    
   </div>
</nav>
666
<h4>工具提示（Tooltip）插件 - 锚</h4>
这是一个 <a href="#" class="tooltip-test" data-toggle="tooltip" 
   title="默认的 Tooltip">
   默认的 Tooltip
</a>.
这是一个 <a href="#" class="tooltip-test" data-toggle="tooltip" 
   data-placement="left" title="左侧的 Tooltip">
   左侧的 Tooltip
</a>.
这是一个 <a href="#" data-toggle="tooltip" data-placement="top" 
   title="顶部的 Tooltip">
   顶部的 Tooltip
</a>.
这是一个 <a href="#" data-toggle="tooltip" data-placement="bottom" 
   title="底部的 Tooltip">
   底部的 Tooltip
</a>.
这是一个 <a href="#" data-toggle="tooltip" data-placement="right" 
   title="右侧的 Tooltip">
   右侧的 Tooltip
</a>

<br>

<h4>工具提示（Tooltip）插件 - 按钮</h4>
<button type="button" class="btn btn-default" data-toggle="tooltip" 
   title="默认的 Tooltip">
   默认的 Tooltip
</button>
<button type="button" class="btn btn-default" data-toggle="tooltip" 
   data-placement="left" title="左侧的 Tooltip">
   左侧的 Tooltip
</button>
<button type="button" class="btn btn-default" data-toggle="tooltip" 
   data-placement="top" title="顶部的 Tooltip">
   顶部的 Tooltip
</button>
<button type="button" class="btn btn-default" data-toggle="tooltip" 
   data-placement="bottom" title="底部的 Tooltip">
   底部的 Tooltip
</button>
<button type="button" class="btn btn-default" data-toggle="tooltip" 
   data-placement="right" title="右侧的 Tooltip">
   右侧的 Tooltip
</button>

    <script>
    $(function () { $("[data-toggle='tooltip']").tooltip(); });
    </script>
