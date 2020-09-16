<template>
  <div id="root" class="root">
    <router-view></router-view>
  </div>
</template>

<script>
  export default {}
</script>

<style lang="scss">
  #root{
    width: 100%;
    height: 100%;
  }
  #elTable{
    max-height: 450px;
    overflow-y: scroll;
  }
  .el-table td, .el-table th{
    padding: 6px 0!important;
  }
  .el-pagination{
    padding: 15px 5px 4px 5px;
  }
  .el-form-item{
    margin-bottom: 10px;
  }
  .content-wrapper{
    padding: 12px 16px!important;
  }
  a {
    text-decoraction: none!important;
  }
  .router-link-active {
    text-decoration: none!important;
  }
  input[type="text"].el-select__input {
    border: none;
    background: none;
  }
</style>
