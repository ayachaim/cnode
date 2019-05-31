<template>
  <div class="Header">
    <img src="../assets/cnodejs_light.svg" alt="cnode">
    <div class="search"><img src="" alt="search"></div>
    <ul>
      <li><a href="">首页</a></li>
      <li><a href="">新手</a></li>
      <li><a href="">API</a></li>
      <li><a href="">关于</a></li>
      <li><a href="">登录</a></li>
      <li><a href="">注册</a></li>
    </ul>
  </div>

</template>
<script>
export default {
  name: 'Header'
}
</script>
<style scoped>
.Header{
  background-color: #5a5555;
  height:50px;
}

img{
  float:left;
  max-width:120px;
  margin-left:50px;
  margin-top:8px;
}
ul{
  list-style: none;
  float:right;
}
li{
  display:inline-block;
  padding:10px;
  margin-top: 10px;
  margin-right:20px;
  color:white;
}
a{
  text-decoration: none;
  color:white;
}
.search{
  height:30px;
  width:150px;
  background-color: white;
  float:left;
  margin-top: 12px;
  margin-left:200px;
  border-radius: 6px;

}

</style>
