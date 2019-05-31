<template>
<!--loading视图-->
<div class="PostList">
  <div class='isloading' v-if="isLoading">
    <img src="../assets/timg.jpg">
  </div>
  <!--帖子视图-->
  <div class="view" v-else>
    <div class="topbar">
      <span>全部</span>
      <span>精华</span>
      <span>分享</span>
      <span>问答</span>
      <span>招聘</span>
      <span>客户端测试</span>
    </div>
    <div class="posts">
      <ul class="ulList">
        <li v-for="post in posts" class="wapper_li">
          <img :src="post.author.avatar_url"  class="img">

          <span class="visit_count">
            <span class="replay-count">{{post.reply_count}}</span>
            /{{post.visit_count}}
          </span>
          <span :class="[{put_good:(post.good==true),put_top:(post.top==true),topList:(post.good!==true && post.top!==true)}]">
            <span class="tab">
              {{  post | tabFormat}}
            </span>
          </span>
          <router-link :to="{name:'request_content',params:{id:post.id}}">
          <span class="title">
            {{post.title}}
          </span>
          </router-link>
          <span class="time">
            {{post.last_reply_at | formatDate}}
          </span>
        </li>
      </ul>
    </div>
  </div>
  </div>
</template>
<script>
export default {
  name: 'PostList',
  data () {
    return {
      isLoading: false,
      posts: []
    }
  },
  methods: {
    getData () {
      this.$http.get(`https://cnodejs.org/api/v1/topics`, {
        page: 1,
        limit: 15
      })
        .then(res => {
          this.isLoading = false
          this.posts = res.data.data
        })
        .catch(err => {
          console.log(err)
        })
    }
  },
  beforeMount () {
    this.isLoading = true
    this.getData()
  }

}
</script>
<style >
.img{
  width:30px;
  height:30px;
  vertical-align: middle;
  margin:10px;
}
.put_good{
background-color:#999;
border-radius: 1px;
}
.tab{
  font-size:13px;
}
.put_top{
  background-color:#80bd01;
  border-radius: 1px;

}
.topList{
  background-color:#999;
border-radius: 1px;

}
.ulList{
  list-style: none;
  background-color: #f5efef;
}
.view{
  display:block;
  background-color: #f6f6f6;
  border-radius: 8px;
}
.topbar{
  margin:5px 10px;
  font-size:14px;
  color:#80bd01;
  padding: 8px 12px;

}
.replay-count{
  color:#b4b4b4;
  font-size: 10px;
}
.visit_count{
  color:#9e78c0;
  font-size: 10px;
}
.title{
  display:inline;
  color:#333;
  vertical-align: middle;
  width:100%;
  line-height: 30px;
  font-size:15px;
  text-overflow:ellipsis;
  white-space: nowrap;
  overflow: hidden;
  text-decoration:none;

}
.wapper_li{
  position:relative;

}
.time{
  color:#333;
  vertical-align: middle;
  white-space: nowrap;
  line-height: 30px;
  font-size:15px;
  text-align: right;
  position:absolute;
  right:0;
  margin:0 4px;
}

</style>
