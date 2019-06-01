<template>
  <div class='isloading' v-if="isLoading">
    <img src="../assets/timg.jpg">
  </div>
  <div v-else class="warpper_content">
    <div class="topic_header">
      <div class="topic_title">{{post.title}}</div>
      <ul class="ul_list">
        <li>*发布于{{post.create_at | formatDate }}</li>
        <li>*作者:{{post.author.loginname}}</li>
        <li>*浏览量：{{post.visit_count}}</li>
        <li>*来自：{{post |tabFormat}}</li>
      </ul>
    </div>
    <div v-html="post.content" class="post_content">
    </div>
    <br>
    <hr>
    <br>
    <div id="reply">
      <div class="topbar">回复</div>
      <div v-for="(reply,index)  in post.replies" class="replySec">
        <div class="replyUp">
          <router-link :to="{
          name:'user_info',
          params:{
            name:reply.author.loginname
          }
          }">
            <img :src="reply.author.avatar_url" alt="">
          </router-link>
          <router-link :to="{
          name:'user_info',
          params:{
            name:reply.author.loginname
          }
          }">
            <span>{{reply.author.loginname}}</span>
          </router-link>
          <span>
          {{index+1}}楼
        </span>
          <span v-if="reply.ups.length>0" >
          ☝ {{reply.ups.length}}
        </span>
          <span v-else>
        </span>
        </div>
      <p v-html="reply.content"></p>
      </div>
      </div>
  </div>
</template>
<script>
export default {
  name: 'Article',
  data () {
    return {
      isLoading: false,
      post: []
    }
  },
  methods: {
    getTopiclist () {
      this.$http.get(`https://cnodejs.org/api/v1/topic/${this.$route.params.id}`)
        .then(res => {
          if (res.data.success == true) {
            this.isLoading = false
            this.post = res.data.data
          }
        })
        .catch(err => {
          console.log(err)
        })
    }
  },
  beforeMount () {
    this.isLoading = true
    this.getTopiclist()
  }
}
</script>
<style scoped>
@import url('../assets/markdown-github');
.warpper_content{
  background-color:white;
  width:70%;
  height:70%;
  overflow:hidden;
  margin:10px 0;
}
.ul_list{
  list-style: none;
  color:#838383;
  font-size:12px;
  margin:5px 10px;

}
li{
  display:inline;
}
.topic_header{
  width:100%;
  height:100%;
  margin:15px auto;

}
.topic_title{
  font-weight:bold;
  font-size:20px;
  padding: 20px 25px;
}
.post_content{
  width:100%;
  height:100%;
  font-size:15px;
  font-weight:300;
  color:#333;
}
.img{
  width:200px;
  height:200px;
}
</style>
