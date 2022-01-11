<template>
  <div>
    <h1>评论</h1>
    <div class="input-container">
      <input type="textarea" placeholder="输入评论内容" v-model="content" />
      <button @click="addCommentClick">添加</button>
    </div>
  </div>
</template>

<script>
import {nanoid} from 'nanoid'
import dayjs from 'dayjs'
  let COMMENT = 'comment'
  export default {
    data() {
      return {
        content: ''
      }
    },
    methods: {
      addCommentClick() {
        if(this.content === '') {
          alert('请输入内容');
        } else {
          if(window.localStorage.getItem(COMMENT)) {
            let commentList = JSON.parse(window.localStorage.getItem(COMMENT));
            commentList.push({
                id: nanoid(),
                content: this.content,
                time: dayjs(Date.now()).format('MM/DD/YYYY hh:mm'),
                replys: []
            });
            window.localStorage.setItem(COMMENT, JSON.stringify(commentList));
          } else {
            window.localStorage.setItem(COMMENT, JSON.stringify([{
                id: nanoid(),
                content: this.content,
                time: dayjs(Date.now()).format('MM/DD/YYYY hh:mm'),
                replys: []
            }]))
          }
          window.history.go(0);
        }

      }
    },
  }
</script>

<style lang="less" scoped>
.input-container{
  display: flex;
  flex-direction: column;
  input {
    width: 400px;
    height: 200px;
  }
  button {
    width: 80px;
    height: 30px;
    margin: 20px 0;
  }
}
</style>