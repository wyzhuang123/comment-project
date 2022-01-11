<template>
  <div style="width: 40%">
    <comment-input/>
    <comments/>
  </div>
</template>

<script>
import commentInput from './comment/commentInput.vue'
import Comments from './comment/comments.vue'
  
  export default {
  components: { commentInput, Comments },
    
  }
</script>

<style lang="less" scoped>

</style>