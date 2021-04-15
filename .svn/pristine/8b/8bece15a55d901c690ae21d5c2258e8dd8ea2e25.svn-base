
<!-- 模块：变更 -->

<template>
  <div class="comTableBox" style="margin-top: 0;">

    <div class="comTableTitle">
      <span>变更说明</span>
    </div>

    <div class="formLine">
      <!-- 变更原因 -->
      <div class="formLabel">变更原因：</div>
      <div class="formText">
        {{examineGoodsModify.modify_reason}}
      </div>
    </div>
    <div class="formLine">
      <!-- 变更内容 -->
      <div class="formLabel">变更内容：</div>
      <div class="formText">
        {{examineGoodsModify.modify_content}}
      </div>
    </div>

  </div>
</template>

<script>
import { mapState } from 'vuex'
export default {
  data() {
    return {}
  },
  computed: {
    ...mapState(['examineGoodsModify'])
  }
}
</script>

<style scoped>
.comTableBox {
  margin-bottom: 5px;
  border-top: 1px solid #DCDFE6;
}
.comTableTitle {
  color: #409EFF;
  font-size: 14px;
  padding: 10px;
  background: #ecf5ff;
  flex: 1;
}

.formLine { /* 单行 */
  width: 100%;
  font-size: 12px;
  display: flex;
}
.formLabel { /* 标题 */
  width: 110px;
  min-height: 34px;
  padding: 0 4px;
  border-right: 1px solid #DCDFE6;
  display: flex;
  align-items: center;
  justify-content: flex-end;
}
.formText { /* 值 */
  padding: 6px 10px;
  border-right: 1px solid #DCDFE6;
  display: flex;
  flex-wrap: wrap;
  align-items: center;
  flex: 1;
}

.input_reason {
  width: 30%;
  min-width: 500px;
}
.input_content {
  width: 50%;
  min-width: 800px;
}
</style>
