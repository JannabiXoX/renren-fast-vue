<template>
  <el-tree
    :data="menus"
    :props="defaultProps"
    node-key="catId"
    ref="menuTree"
    @node-click="nodeClick"
  >
  </el-tree>
</template>

<script>
export default {
  name: 'category.vue',
  data () {
    return {
      menus: [],
      expandedKey: [],
      defaultProps: {
        children: 'childMenu',
        label: 'name'
      }
    }
  },
  created () {
    this.getMenus()
  },
  methods: {
    getMenus () {
      this.$http({
        url: this.$http.adornUrl('/product/category/list/tree'),
        method: 'get'
      }).then(({data}) => {
        console.log('成功获取到菜单数据...', data.page)
        this.menus = data.page
      })
    },
    nodeClick (data, node, component) {
      console.log('子组件category的节点被点击', data, node, component)
      this.$emit('tree-node-click', data, node, component)
    }
  }
}
</script>

<style scoped>

</style>
