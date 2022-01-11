<template>
  <div>
    <div class="comment-container">
      <div class="main-comment">
        <span style="">{{ comment.time }}</span>
        <span style="color: gray; margin-left: 5px" @click="() => {isCommnetReply = false; isComment = !isComment}">
          <i class="iconfont icon-shaixuanjiantoushang"></i>
          </span>
        
        <p style="font-size: 20px; font-weight: 600" v-show="isComment">{{ comment.content }}</p> 
      </div>
      <div>
        <span style="color: gray; margin-left: 5px" @click="isCommnetReply = !isCommnetReply" >
            <i class="iconfont icon-shaixuanjiantoushang"></i>
            <i>回复</i>
        </span>
      </div>
      <div class="comment-reply" v-show="isCommnetReply">
        <div v-for="(reply, index) in comment.replys" :key="index" class="reply-item">
          <span style="">{{ reply.time }}</span>
          <p style="font-weight: 600">{{ reply.content }}</p>
        </div>
      </div>
      <a href="" @click.stop.prevent="() => {isReply = !isReply}　" v-if="!isReply">回复</a>
      <div v-if="isReply">
        <input type="textarea" v-model="replyValue"><br/>
        <button @click.stop.prevent="replyClick(comment.id)">发送</button>
        <button @click="() => {isReply = !isReply}">取消</button>
      </div>
    </div>
  </div>
</template>

<script>
import dayjs from 'dayjs'
import '@/assets/font.css'
  export default {
    data() {
      return {
        isComment: true,
        isCommnetReply: false,
        isReply: false,
        replyValue: ''
      }
    },
    methods: {
      replyClick(id) {
        if(this.replyValue === '') {
          alert('请输入回复内容');
          return;
        } 
        let commentList = JSON.parse(window.localStorage.getItem('comment'));
        commentList.forEach((comment) => {
          if(comment.id === id) {
              comment.replys.push({
                content: this.replyValue,
                time: dayjs(Date.now()).format('MM/DD/YYYY hh:mm')
              })
              window.localStorage.setItem('comment', JSON.stringify(commentList));
              this.isReply = !this.isReply;
              window.history.go(0);
            }
        })
      }
    },
    props: {
      comment: {
        type: Object,
        required: true
      }
    },
  }
</script>

<style lang="less" scoped>
.comment-container{
  display: flex;
  flex-direction: column;
  margin: 20px 10px;
  border-bottom: 1px solid black;
  .comment-reply{
    padding: 0 20px;
    margin-top: 10px;
    .reply-item{
      margin: 10px 0;
    }
  }
}
</style>