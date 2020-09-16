<template>
  <div class="filter">
    <el-row>
      <el-col :span="24">
        <el-table size="mini" :data="master_user.data" border style="width: 100%" highlight-current-row>
          <el-table-column prop="index" label="序号" width="60">
            <template slot-scope="{row,$index}">
              <span>{{$index + 1}}</span>
            </template>
          </el-table-column>
          <el-table-column v-for="(item,index) in master_user.columns" :label="item.label" :prop="item.prop" :width="item.width">
            <template slot-scope="scope">
             <span v-if="scope.row.isSet">
               <el-input size="mini" placeholder="请输入内容" v-model="master_user.data[scope.$index][item.prop]">
               </el-input>
             </span>
              <span v-else>{{scope.row[item.prop]}}</span>
            </template>
          </el-table-column>
          <el-table-column label="操作" width="">
            <template slot-scope="scope">
<!--             <span class="el-tag el-tag&#45;&#45;success el-tag&#45;&#45;mini" style="cursor: pointer;" @click.stop="saveRow(scope.row,scope.$index)">-->
<!--               确定-->
<!--             </span>-->
              <span class="el-tag el-tag--primary el-tag--mini" style="cursor: pointer;" @click="editRow(scope.row,scope.$index)">
               编辑
             </span>
              <span class="el-tag el-tag--danger el-tag--mini" style="cursor: pointer;" @click="deleteRow(scope.$index,master_user.data)">
               删除
             </span>
            </template>
          </el-table-column>
        </el-table>
      </el-col>

        <el-col :span="12" :gutter="30">
          <div class="el-table-add-row" style="width: 99.2%;" @click="add()"><span>+ 添加</span></div>
        </el-col>
        <el-col :span="12">
          <div class="el-table-add-row" style="width: 99.2%;" @click="saveData()"><span>+保存</span></div>
        </el-col>
    </el-row>
    <!--    <span>{{master_user.data}}</span>-->
  </div>
</template>
<script>
  export default {
    data() {
      return {
        master_user: {
          // 选中行
          sel: null,
          columns: [{
            prop: 'type',
            label: '远程类型',
            width: 120
          },
            {
              prop: 'addport',
              label: '连接地址',
              width: 150
            },
            {
              prop: 'user',
              label: '登录用户',
              width: 120
            },
            {
              prop: 'pwd',
              label: '登录密码',
              width: 220
            },
            {
              prop: 'info',
              label: '其他信息'
            }
          ],
          data: []
        }
      }
    },
    methods: {
      add() {
        let j = {
          'type': '',
          'addport': '',
          'user': '',
          'pwd': '',
          'info': '',
          'isSet': true
        };
        this.master_user.data.push(j);
      },
      saveData(row, index) {
        // 保存
        for(var x in this.master_user.data){
          this.master_user.data[x].isSet = false;
        }
        console.log('000',this.master_user.data)
      },
      editRow(row,index) {
        let isInput=row.isSet;
        if(isInput){
          this.$message.warning('请先保存当前编辑项');
        }else{
          row.isSet=true;
        }
      },
      deleteRow(index, rows) {
        // 删除
        rows.splice(index, 1)
      }
    }
  };
</script>
<style lang="scss" scoped>
  .el-table-add-row {
    margin-top: 10px;
    width: 100%;
    height: 34px;
    border: 1px dashed #c1c1cd;
    border-radius: 3px;
    cursor: pointer;
    justify-content: center;
    display: flex;
    line-height: 34px;
  }
</style>
