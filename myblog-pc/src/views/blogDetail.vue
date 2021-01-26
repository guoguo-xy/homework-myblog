<template>
  <div class="container">
    <div class="blog">
      <div class="blog-title">
        <h3>{{ blog.title }}</h3>
        <span>{{ blog.post_time }}</span>
      </div>
      <div class="blog-content">{{blog.content}}</div>
      <div class="comments">
        <h3>评论:</h3>
        <div class="comment" v-for="(item,index) in blog.comments" :key="item.comm_id">
          <!-- <span>{{index +1}}</span> -->
          <div class="comment-content">{{index +1}}.{{item.comm_content}}</div>
          <div class="comment-info">
            <span class="userinfo">{{item.username}}</span>
            <span class="post-time">{{item.comm_post_time}}</span>
          </div>
        </div>
        <div class="add-comment">
          <input class="add-info" name="inpVal" type="text" v-model="inpVal"> 
          <button class="add-btn" @click="addComm()">添加评论</button>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      blog:'',
      inpVal:'',
    
    };
  },
  created() {
    this.getBlogDetail();
  },
  methods: {
    getBlogDetail() {
      let blogId = this.$route.params.blogId;
      this.$http.get("/blog/detail/",{
        params: {
          blogId: blogId,
        },
      })
        .then((res) => {
          let { state, blog } = res.data;
          if (state == "success") {
            this.blog = blog;
          }
        })
    },
    addComm(){
      console.log(this.blog);
      this.$http
        .post("/blog/addComm",{
          inpVal:this.inpVal,
          blogId:this.blog.blog_id    
        }).then((res)=>{
          console.log(res);
          this.getBlogDetail()
        });
    
    }
  },
};
</script>

<style scoped>
.blog {
    width: 1000px;
    margin: 20px auto;
    padding: 20px;
    background: #cccccc;
}

.blog-title {
    padding: 10px;
    text-align: center;
    /* border-bottom: 1px solid #000; */
}

.blog-content {
    padding: 10px;
    text-align: center;
    border: #000 1px solid;
}

.comment-title {
    padding: 10px;
    margin-bottom: 5px;
    position: relative;
}

.comment {
    padding: 20px;
    margin-bottom: 5px;
}

.comment-info {
    float: right;
}

.userinfo {
    padding-right: 5px;
}
.add-comment{
  border-top: 1px solid #000;
  padding: 10px;
  
  
}
.add-info{
  border: #000 1px solid;
  border-radius: 2px;
  width: 850px;
  height: 30px;
  line-height: 30px;
}
.add-btn{
  float: right;
  width: 80px;
  height: 30px;
  line-height: 30px;
}

</style>
