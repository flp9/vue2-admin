<template>
  <div class="log">
    <h4>操作日志</h4>
    <el-tree
      :data="data"
      :props="defaultProps"
      accordion
      @node-click="handleNodeClick"
      :render-content="renderContent"
    >

    </el-tree>
  </div>
</template>
<script>
  export default {
    data() {
      return {
        data: [{
          label: '一级 1',
          children: [
            {label: '二级 1-1'}, {label: '二级 1-2'}, {label: '二级 1-3'}
          ]
        }, {
          label: '一级 2',
          children: [{
            label: '二级 2-1',
            children: [{
              label: '三级 2-1-1'
            }]
          }, {
            label: '二级 2-2',
            children: [{
              label: '三级 2-2-1'
            }]
          }]
        }, {
          label: '一级 3',
          children: [{
            label: '二级 3-1',
            children: [{
              label: '三级 3-1-1'
            }]
          }, {
            label: '二级 3-2',
            children: [{
              label: '三级 3-2-1'
            }]
          }]
        }],
        defaultProps: {
          children: 'children',
          label: 'label'
        }
      };
    },
    methods: {
      handleNodeClick(data) {
        console.log(data);
      },
      renderContent(h, { node, data, store }) {
        console.log('node', node)
        console.log('data', data)
        console.log('store', store)
        if (!node.data.children) {
          console.log('00000')
          return (
            <p> {node.data.label} 详 情</p>
          )
        } else {
          return (
            <span class="custom-tree-node">
              <span>{node.label}</span>
            </span>
          )
        }
      }
    }
  };
</script>
<style lang="scss" scoped>

</style>
