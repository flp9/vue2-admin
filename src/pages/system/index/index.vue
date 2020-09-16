<template>
  <div class="index">
    <button @click="toLink">日历插件，点击进入</button>
    <el-row>
      <el-col :span="20" :offset="2">
        <el-calendar v-model="data">
        </el-calendar>
      </el-col>
    </el-row>

  </div>
</template>
<script>
  export default {
    data() {
      return {
        data: new Date()
      }
    },
    created() {
      console.log('000-----', this.data)
    },
    methods: {
      toLink() {
        this.$router.replace('../CalendarTest');
      }
    }
  }
</script>
<style lang="scss" scoped>
  .is-selected {
    color: #1989FA;
  }
</style>
