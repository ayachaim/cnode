<template>
  <div id="app">
    <Header></Header>
    <div class="warpper">
      <router-view name="main"></router-view>
    </div>
  </div>
</template>

<script>
import Header from './components/header'
import PostList from './components/PostList'
export default {
  name: 'App',
  components: {
    Header, PostList
  }
}

</script>

<style>
*{
  margin:0;
  padding: 0;
}
#app{
  background-color: #e1e1e1;
}
.warpper{
  width:90%;
  height:90%;
  margin:0 auto;

}

</style>
