<template>
  <li class="todo-line">
    <h3 @mouseenter="showDeleteTag" @mouseleave="hideDeleteTag">
      <input type="checkbox" @click="itemCheck(item)">
      <p class="item-label">{{item}} {{ index+1}}</p>
      <p class="item-status" v-if="checked">已完成</p>
      <p class="item-delete" v-if="isShowDeleteTag" @click="deleteClick">Delete</p>
    </h3>
  </li>
</template>

<script>
  export default {
    props:["item","index"],
    data () {
      return {
        isShowDeleteTag: false,
        checked: false
      }
    },
    methods: {
      itemCheck () {
        this.checked = !this.checked
      },
      deleteClick () {
        // 触发该项自定义事件delete
        this.$emit('delete', this.index)
      },
      showDeleteTag () {
        this.isShowDeleteTag = true
      },
      hideDeleteTag () {
        this.isShowDeleteTag = false
      }
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .todo-line {
    height: 30px;
    line-height: 30px;
    list-style: none;
  }
  h3{
    width: 400px;
    margin:0 auto;
    color: black;
    background: gainsboro;
  }
  .item-status {
    display: inline;
    background: red;
    color: white;
    padding: 0 5px;
    font-size: 12px;
  }
  .item-delete {
    display: inline;
    text-decoration: underline;
    font-size: 12px;
    color: gray;
    cursor: pointer;
  }
  .item-label {
    display: inline;
  }
</style>
