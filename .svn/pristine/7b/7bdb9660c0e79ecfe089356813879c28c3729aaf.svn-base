
<!-- 模块：表格 -->

<template>
  <div class="comTableBox">
    <div class="comTableTitle">
      <span>分仓验货明细</span>
    </div>
    <el-table :data="tableList" border :header-cell-style="{ background: 'none' }" :span-method="objectSpanMethod">
      <!-- 仓库 -->
      <el-table-column label="仓库" align="center" width="150">
        <template slot-scope="scope">
          <div class="comCell">
            <span>{{scope.row.store_name}}</span>
          </div>
        </template>
      </el-table-column>
      <!-- 验货日期 -->
      <el-table-column label="验货日期" align="center" width="160">
        <template slot-scope="scope">
          <div class="comCell">
            {{scope.row.examine_time}}
          </div>
        </template>
      </el-table-column>
      <!-- 验货人 -->
      <el-table-column label="验货人" align="center" width="150">
        <template slot-scope="scope">
          <div class="comCell">
            {{scope.row.examine_name}}
          </div>
        </template>
      </el-table-column>
      <!-- 验货结果 -->
      <el-table-column label="验货结果" align="center" width="150">
        <template slot-scope="scope">
          <div class="comCell">
            {{{ 0: '不合格', 1: '合格' }[scope.row.examine_result]}}
          </div>
        </template>
      </el-table-column>
      <el-table-column label="不合格原因" align="center">
        <!-- 原因类型 -->
        <el-table-column label="原因类型" align="center" width="150">
          <template slot-scope="scope">
            <div class="comCell">
              {{arrResultType[scope.row.reason_type] ? arrResultType[scope.row.reason_type].label : ''}}
            </div>
          </template>
        </el-table-column>
        <!-- 原因描述 -->
        <el-table-column label="原因描述" align="center" width="150">
          <template slot-scope="scope">
            <div class="comCell">
              <span v-for="(viewItem, viewIndex) in (arrResultType[scope.row.reason_type] ? arrResultType[scope.row.reason_type].arr : [])" :key="'view_' + viewIndex"
                v-show="viewItem.value === scope.row.reason_desc"
              >
                {{viewItem.label}}
              </span>
            </div>
          </template>
        </el-table-column>
        <!-- 比例 -->
        <el-table-column label="比例（%）" align="center" width="120">
          <template slot-scope="scope">
            <div class="comCell">
              {{scope.row.ratio}}
            </div>
          </template>
        </el-table-column>
        <!-- 责任归属 -->
        <el-table-column label="责任归属" width="400">
          <template slot-scope="scope">
            <div class="comCell">
              <div class="comCheckboxBox">
                <span class="comCheckboxLabel">内部：</span>
                <el-checkbox-group v-model="scope.row.accountability.in" disabled>
                  <el-checkbox :label="item.label" v-for="item in arrIn" :key="'out_' + item.label">{{item.text}}</el-checkbox>
                </el-checkbox-group>
              </div>
              <div class="comCheckboxBox">
                <span class="comCheckboxLabel">外部：</span>
                <el-checkbox-group v-model="scope.row.accountability.out" disabled>
                  <el-checkbox :label="item.label" v-for="item in arrOut" :key="'out_' + item.label">{{item.text}}</el-checkbox>
                </el-checkbox-group>
              </div>
            </div>
          </template>
        </el-table-column>
        <!-- 归属说明 -->
        <el-table-column label="归属说明" align="center" width="150">
          <template slot-scope="scope">
            <div class="comCell">
              {{scope.row.detail_explain}}
            </div>
          </template>
        </el-table-column>
      </el-table-column>
      <!-- 处理方式 -->
      <el-table-column align="center" width="150">
        <template slot="header" slot-scope="scope">
          处理方式
        </template>
        <template slot-scope="scope">
          <div class="comCell">
            {{scope.row.handle_mode}}
          </div>
        </template>
      </el-table-column>
      <!-- 备注 -->
      <el-table-column label="备注" align="center" width="150">
        <template slot-scope="scope">
          <div class="comCell">
            {{scope.row.remark}}
          </div>
        </template>
      </el-table-column>
      <!-- 验货报告 -->
      <el-table-column label="验货报告" min-width="400">
        <template slot-scope="scope">
          <div class="comCell">
            <el-upload class="asd" action="#" multiple :file-list="scope.row.fileList" disabled :on-preview="uploadLook"></el-upload>
          </div>
        </template>
      </el-table-column>
    </el-table>

  </div>
</template>

<script>
import { mapState } from 'vuex'
export default {
  props: ['pageType'],
  data() {
    return {
      id: ''
    }
  },
  created() {},
  computed: {
    ...mapState(['arrResult', 'arrResultType', 'arrOut', 'arrIn', 'arrHandlingType']),
    ...mapState({
      tableData(state) {
        const { pageType = '' } = this
        return state[`tableData_${pageType}`] || []
      },
      storehouse(state) {
        const { pageType = '' } = this
        return state[`storehouse_${pageType}`] || []
      }
    }),
    tableList() {
      const { pageType = '' } = this
      const obj = this.$store.getters[`tableList_${pageType}`] || {}
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
    objectSpanMethod({ row, column, rowIndex, columnIndex }) {
      const { tableData } = this
      if (columnIndex < 5 || columnIndex > 10) {
        if (!row.key) {
          const { store_name = '新增仓库', index } = row
          let length = 0
          for (let i = 0; i < tableData[`${index}.${store_name}`].length; i++) {
            const item = tableData[`${index}.${store_name}`][i]
            if (item.is_delete !== '0') {
              length++
            }
            // if (i === 0 && String(item.examine_result) === '1') {
            //   break
            // }
          }
          return { rowspan: length, colspan: 1 } // 合并
        } else {
          return { rowspan: 0, colspan: 0 } //      隐藏
        }
      }
    }
  }
}
</script>

<style scope>
.comTableBox {
  margin-top: 5px;
  border-top: 1px solid #DCDFE6;
}
.comTableTitle {
  color: #409EFF;
  font-size: 14px;
  padding: 10px;
  background: #ecf5ff;
  flex: 1;
}

/*** 表格 ***/
.comCell { /* 单元格内：容器 */
  padding: 2px 10px;
}
.comCheckboxBox { /* 多选框：容器 */
  display: flex;
}
.comCheckboxLabel { /* 多选框：标题 */
  white-space: nowrap;
}
.comCell > .comCheckboxBox:first-child {
  margin-bottom: 4px;
}
</style>

<style>
/*** 多选框 ***/
.comCheckboxBox > .el-checkbox-group { /* 选项组 */
  line-height: 10px;
}
.comCheckboxBox > .el-checkbox-group > .el-checkbox { /* 选项 */
  margin-right: 20px;
}
.comCheckboxBox > .el-checkbox-group > .el-checkbox > .el-checkbox__label { /* 选项：文字 */
  font-size: 12px !important;
  padding-left: 5px;
}
.is-checked > .el-checkbox__inner {
  background-color: #409EFF !important;
  border-color: #409EFF !important;
}
</style>
