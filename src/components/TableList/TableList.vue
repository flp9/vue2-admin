<template>
    <div class="table-list">
<!--      搜索弹窗-->
      <el-form :inline="true"  class="demo-form-inline">
        <el-form-item>
          <el-input v-model="input" placeholder="请输入内容"  size="small"></el-input>
        </el-form-item>
        <el-form-item>
          <el-button type="primary" icon="el-icon-search" :loading="true"  size="small" @click="onSubmit">搜索</el-button>
        </el-form-item>
      </el-form>
<!--表格内容区-->
      <el-table
        :data="tableListDataAll.tableListData.slice((currentPage-1)*pageSize,currentPage*pageSize)"
        style="width: 100%" id="elTable">
<!--        序号-->
        <el-table-column prop="index" label="序号" width="60">
          <template slot-scope="{row,$index}">
            <span>{{$index + 1}}</span>
          </template>
        </el-table-column>
<!--表格列表头部标题-->
        <el-table-column v-for="item in tableListDataAll.columnsTitle"
          :label="item.label"
          :prop="item.prop"
          :width="item.width"
        >
          <template slot-scope="scope">
            <span style="margin-left: 10px">{{ scope.row[item.prop] }}</span>
          </template>
        </el-table-column>
<!--操作-->

        <el-table-column label="操作" prop="edit">
          <template slot-scope="scope">
            <el-button
              size="mini"
              @click="handleEdit(scope.$index, scope.row)">编辑</el-button>
            <el-button
              size="mini"
              type="danger"
              @click="handleDelete(scope.$index, scope.row)">删除</el-button>
          </template>
        </el-table-column>

      </el-table>

      <!--分页-->
      <el-pagination
        @size-change="handleSizeChange"
        @current-change="handleCurrentChange"
        :current-page="currentPage"
        :page-sizes="[5, 10, 20, 40]"
        :page-size="pageSize"
        layout="total, sizes, prev, pager, next, jumper"
        :total="tableListDataAll.tableListData.length">
      </el-pagination>

      <!--编辑弹窗-->
      <el-dialog title="编辑" :visible.sync="editFormVisible" :close-on-click-modal="false" class="edit-form" :before-close="handleClose" :append-to-body="true">
        <el-form :model="editForm" label-width="80px">
          <el-form-item label="名称" prop="name">
            <el-input v-model="editForm.name" auto-complete="off"></el-input>
          </el-form-item>
          <el-form-item label="日期" prop="date">
            <el-input v-model="editForm.date" auto-complete="off"></el-input>
          </el-form-item>
          <el-form-item label="地址" prop="address">
            <el-input v-model="editForm.address" auto-complete="off"></el-input>
          </el-form-item>
        </el-form>
        <div slot="footer" class="dialog-footer">
          <el-button @click="editFormVisible = false">取消</el-button>
          <el-button type="primary" @click="editSure">确定</el-button>
        </div>
      </el-dialog>
    </div>
</template>

<script>
    export default {
      name: 'TableList',
      created () {
        this.getTableData();
      },
      data() {
        return {
          // 默认不显示编辑弹层
          editFormVisible: false,
          input: '',
          currentPage: 1,
          pageSize: 10,
          // 编辑谈层初始化
          editForm: {
            name: '',
            date: '',
            address: ''
          },
          tableListDataAll: {
            columnsTitle: [{
              prop: 'date',
              label: '日期',
              width: 190
            }, {
              prop: 'name',
              label: '姓名',
              width: 190
            }, {
              prop: 'address',
              label: '地址',
              width: 390
            }],
            // 表格主体内容
            tableListData: []
          }

        }
      },
      methods: {
        getTableData () {
          this.axios.get('../../../static/testLists.json')
            .then(res => {
              this.tableListDataAll.tableListData = res;
            })
            .catch(error => {
              console.log(error);
            });
        },
        handleEdit(index, row) {
          this.editFormVisible = true;
          // 编辑弹窗初始化赋值
          this.editForm = Object.assign({}, row);
          this.tableListDataAll.tableListData.splice(index, 1, this.editForm);
        },
        handleDelete(index, row) {
          this.tableListDataAll.tableListData.splice(index, 1)
          console.log(index, row);
        },
        handleSizeChange(size) {
          this.pageSize = size;
          // 每页下拉显示数据
          console.log(this.pageSize)
        },
        handleCurrentChange(currentPage) {
          this.currentPage = currentPage;
          // 点击第几页
          console.log(this.currentPage)
        },
        handleClose(done) {
          this.editFormVisible = false;
          // this.confirm('确认关闭？')
          //   .then(_ => {
          //     done();
          //   })
          //   .catch(_ => {});
        },
        editSure() {
          this.editFormVisible = false;
        },
        onSubmit() {

        }
      }
    }
</script>

<style scoped>

</style>
