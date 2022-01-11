<template>
  <div>
    <h1>评论区</h1>
    <div>
      <comment v-for="item in commentList" :key="item.id" :comment="item"/>
    </div>
  </div>
</template>

<script>
import Comment from './comment.vue';
  export default {
  components: { Comment },
    data() {
      return {
        commentList: [],
      }
    },
    methods: {
      initCommentData() {
        if(window.localStorage.getItem('comment')) {
          this.commentList = JSON.parse(window.localStorage.getItem('comment'));
        }
      }
    },
    created () {
      this.initCommentData();
    },
  }
</script>

<style lang="less" scoped>
</style>