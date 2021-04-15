
<!-- 模块：表单 -->

<template>
  <div class="comTableBox" style="margin-top: 0;">

    <div class="comTableTitle">
      <span>录入验货报告</span>
    </div>

    <div class="formLine">
      <!-- 项目信息 -->
      <div class="formLabel">项目信息：</div>
      <div class="formText">
        {{examineGoods.item_information}}
      </div>
      <!-- 客户名称 -->
      <div class="formLabel">客户名称：</div>
      <div class="formText formMiniText">
        {{customMap.custom_name}}
      </div>
    </div>

    <div class="formLine">
      <!-- 验货日期 -->
      <div class="formLabel">验货日期：</div>
      <div class="formText">
        {{examineGoods.examine_time}}
      </div>
      <!-- 发货方式 -->
      <div class="formLabel">发货方式：</div>
      <div class="formText formMiniText">
        {{deliveryType[examineGoods.deliver_type !== null ? examineGoods.deliver_type : customMap.delivery_type]}}
      </div>
      <!-- 综合验货结果 -->
      <div class="formLabel">综合验货结果：</div>
      <div class="formText formMiniText">
        {{{ 1: '合格', 0: '不合格' }[examineGoods.final_examine_result]}}
      </div>
      <div class="formText formMiniText">
        {{{ 1: '合格', 0: '不合格' }[examineGoods.final_examine_result]}}
      </div>
    </div>

    <div class="formLine">
      <!-- 不合格原因汇总 -->
      <div class="formLabel">不合格原因汇总：</div>
      <div class="formText">
        <div class="summaryBox" v-for="(item, index) in summary" :key="'summary_' + index">
          <p class="summaryTitle">
            {{item[0].index + 1}}. {{item[0].store_name}}不合格情况：
          </p>
          <p class="summaryText" v-for="(val, key) in item" :key="'summary_item_' + key">
            ·
            <!-- 原因类型 -->
            <span v-if="val.reason_type">{{val.typeText}} -> </span>
            <span v-else>[请选择<span class="red">原因类型</span>] -></span>
            <!-- 原因描述 -->
            <span v-if="val.reason_desc">{{val.descText}} -> </span>
            <span v-else>[请选择<span class="red">原因描述</span>] -> </span>
            <!-- 比例 -->
            <span v-if="val.ratio && val.resultNumCount === 100">{{val.ratio}}% -> </span>
            <span v-else-if="val.resultNumCount !== 100"> [请填写<span class="red">正確的比例</span>] -></span>
            <span v-else>[请填写<span class="red">比例</span>] -></span>
            <!-- 处理方式 -->
            <span v-if="val.handle_mode">{{val.handle_mode}} -> </span>
            <span v-else>[请选择<span class="red">处理方式</span>] -></span>
            <!-- 责任归属 -->
            <span v-if="val.outInTextArr && val.outInTextArr.length">
              {{val.outInTextArr.join('、')}}负责
              <span v-if="val.detail_explain">({{val.detail_explain}})</span>
            </span>
            <span v-else>[请选择<span class="red">责任归属</span>]</span>
            <!-- 结尾符号 -->
            <span v-if="key === item.length - 1">。</span>
            <span v-else>；</span>
          </p>
        </div>
      </div>
    </div>

    <div class="formLine">
      <!-- 责任划分 -->
      <div class="formLabel">责任划分：</div>
      <div class="formText">
        <el-table :data="formData" border :span-method="objectSpanMethod2">
          <!-- 类型 -->
          <el-table-column prop="type" label="类型" width="50" align="center"></el-table-column>
          <!-- 类型占比（%） -->
          <el-table-column label="类型占比（%）" width="110" align="center">
            <template slot-scope="scope">
              <span>{{scope.row.typeNum}}</span>
            </template>
          </el-table-column>
          <!-- 岗位名称 -->
          <el-table-column prop="job" label="岗位名称" width="100" align="center"></el-table-column>
          <!-- 岗位占比（%） -->
          <el-table-column label="岗位占比（%）" width="140" align="center">
            <template slot-scope="scope">
              <span>{{scope.row.jobNum}}&nbsp;&nbsp;</span>
              <p class="showNum">({{accountability.jobNum ? accountability.jobNum[scope.row.job] : 0}}%)</p>
            </template>
          </el-table-column>
          <!-- 人员占比（%） -->
          <el-table-column label="人员占比（%）">
            <template slot-scope="scope">
              <div class="tableCell">
                <div class="tablePeople" v-for="(item, index) in scope.row.list" :key="'name_input_' + index">
                  <span>{{item.name}}占比:</span>
                  <span>{{item.num}}&nbsp;&nbsp;</span>
                  <p class="showNum" style="text-align: left; margin-right: 20px;" v-if="accountability.peopleNum[scope.row.job]">
                    ({{accountability.peopleNum[scope.row.job][item.name]}}%)
                  </p>
                </div>
              </div>
            </template>
          </el-table-column>
        </el-table>
      </div>
    </div>

    <div class="formLine">
      <!-- 综合说明 -->
      <div class="formLabel">综合说明：</div>
      <div class="formText">
        <span>{{examineGoods.final_explain}}</span>
      </div>
    </div>

    <div class="formLine">
      <!-- 相关附件 -->
      <div class="formLabel">相关附件：</div>
      <div class="formText">
        <el-upload class="asd" action="#" multiple :file-list="examineGoods.fileList" disabled :on-preview="uploadLook"></el-upload>
      </div>
    </div>

  </div>
</template>

<script>
import { mapState } from 'vuex'
export default {
  props: ['pageType'],
  data() {
    return {
      deliveryType: { 1: '直发', 2: '中转', 3: '普通' }, // 发货方式
      select: '' // 下拉框：值
    }
  },
  computed: {
    ...mapState(['customMap']),
    ...mapState({
      formData(state) {
        const { pageType = '' } = this
        return state[`formData_${pageType}`] || []
      },
      examineGoods(state) {
        const { pageType = '' } = this
        return state[`examineGoods_${pageType}`] || {}
      }
    }),
    accountability() {
      const { pageType = '' } = this
      const obj = this.$store.getters[`accountability_${pageType}`] || {}
      return obj
    },
    summary() {
      const { pageType = '' } = this
      const obj = this.$store.getters[`summary_${pageType}`] || {}
      return obj
    }
  },
  methods: {
    /**
     * [上传附件：查看]
     */
    uploadLook(file) {
      const { is_pic, name, url } = file
      if (is_pic === 1) {
        /* 图片：预览 */
        window.open(url)
      } else {
        /* 文件：下载 */
        const a = document.createElement('a')
        a.href = url
        a.download = name
        a.click()
      }
    },
    /**
     * [合并：表格单元格]
     */
    objectSpanMethod2({ row, column, rowIndex, columnIndex }) {
      // console.log(row, column, rowIndex, columnIndex)
      if (columnIndex === 0 || columnIndex === 1) {
        if (row.count) {
          return { rowspan: row.count, colspan: 1 } // 合并：3行1列
        } else {
          return { rowspan: 0, colspan: 0 } // 其他全部隐藏
        }
      }
    }
  }
}
</script>

<style scoped>
.comTableTitle {
  color: #409EFF;
  font-size: 14px;
  padding: 10px;
  background: #ecf5ff;
  flex: 1;
}

/*** 表单 ***/
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
.formMiniText { /* 短框 */
  width: 200px;
  min-width: 200px;
  flex: 0;
}

/*** 不合格原因汇总 ***/
.summaryBox {
  width: 100%;
}
.summaryTitle { /* 标题 */
  font-size: 14px;
  margin-bottom: 4px;
}
.summaryText { /* 文字 */
  margin-bottom: 4px;
}
.summaryBox > .summaryText:last-child {
  margin-bottom: 10px;
}
.summaryBox:last-child > .summaryText:last-child {
  margin-bottom: 0;
}

/*** 表格 ***/
.tableCell { /* 单元格 */
  padding: 3px 10px;
  border-top: 1px solid #EBEEF5;
}
.tableCell:first-child {
  border: 0;
}
.tablePeople {
  /* margin-right: 25px; */
  display: inline-block;
}
.showNum {
  min-width: 40px;
  display: inline-block;
}

.red {
  color: #F56C6C;
}
</style>

<style>
/*** 上传 ***/
.asd { /* 整体容器 */
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  flex: 1;
}
.asd > .el-upload-list { /* 列表 */
  display: flex;
  flex-wrap: wrap;
}
.asd > .el-upload-list > .el-upload-list__item { /* 单个文件 */
  width: auto !important;
  margin-top: 5px !important;
  margin-right: 10px !important;
  background: #F5F7FA !important;
}
.asd > .el-upload-list > .el-upload-list__item > .el-upload-list__item-name { /* 文件名 */
  margin-right: 25px !important;
}
</style>
