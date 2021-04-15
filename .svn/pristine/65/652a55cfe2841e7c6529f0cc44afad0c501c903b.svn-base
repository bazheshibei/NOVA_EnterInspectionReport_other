
<!-- 录入验货报告 -->

<template>
  <el-tabs type="border-card">
    <el-tab-pane class="elTabPaneBox" label="变更后">
      <div class="pageTopBox">
        <!-- 模块：变更 -->
        <com-change></com-change>
        <!-- 模块：表单 -->
        <com-form pageType="new"></com-form>
        <!-- 模块：表格 -->
        <com-table pageType="new"></com-table>
      </div>
    </el-tab-pane>
    <el-tab-pane class="elTabPaneBox" label="变更前">
      <div class="pageTopBox">
        <!-- 模块：表单 -->
        <com-form pageType="old"></com-form>
        <!-- 模块：表格 -->
        <com-table pageType="old"></com-table>
      </div>
    </el-tab-pane>
  </el-tabs>

</template>

<script>
import ComForm from './components/form.vue' //     模块：表单
import ComTable from './components/table.vue' //   模块：表格
import ComChange from './components/change.vue' // 模块：变更
export default {
  components: { ComForm, ComTable, ComChange },
  data() {
    return {}
  },
  created() {
    const local = JSON.parse(localStorage.getItem('NOVA_examineGoods') || '{}')
    const { examine_modify_id = '8a8a80b677f0f3a20177f2614f440024' } = local
    /** 请求：页面数据 **/
    this.$store.dispatch('A_showViewModify', { examine_modify_id })

    try {
      /* 平台方法 */
      // eslint-disable-next-line
      dg.removeBtn('cancel')
      // eslint-disable-next-line
      dg.removeBtn('saveAndAdd')
      // eslint-disable-next-line
      dg.removeBtn('saveAndClose')
      // eslint-disable-next-line
      dg.removeBtn('saveNoClose')
    } catch (err) {
      //
    }
  }
}
</script>

<style scoped>
.elTabPaneBox {
  height: 100%;
  overflow-y: auto;
}
.pageTopBox {
  width: 100%;
  height: 100%;
  /* height: calc(100% - 40px); */
  /* margin-bottom: 40px; */
  overflow-y: auto;
}
</style>
