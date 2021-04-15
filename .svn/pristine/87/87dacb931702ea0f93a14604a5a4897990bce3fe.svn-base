
import Api from '@/config/api'
import Tool from './tool.js'

/**
 * 生产环境代码
 */
const Prod = {}

/**
 * [请求：查看变更明细]
 */
Prod.A_showViewModify = function (state, commit, examine_modify_id) {
  const name = '查看变更明细'
  const obj = { examine_modify_id }
  const suc = function (res) {
    // console.log('返回的数据 ----- ', res)
    // localStorage.setItem('验货报告', JSON.stringify(res))
    const { examineGoodsNew = {}, examineGoodsOld = {}, customMap = {}, examineGoodsDetailListNew = [], examineGoodsDetailListOld = [], wbzrgs = [], businessPostList = [], examineNoQualifyList = [], yhclfs = [], examineBusinessPostListNew = [], examineBusinessPostListOld = [], examineGoodsModify = {} } = res
    const { tableData: tableData_new, storehouse: storehouse_new } = Tool.returnTableObj(examineGoodsDetailListNew)
    const { tableData: tableData_old, storehouse: storehouse_old } = Tool.returnTableObj(examineGoodsDetailListOld)
    const formData_new = Tool.returnFormData(examineBusinessPostListNew, examineGoodsNew, businessPostList)
    const formData_old = Tool.returnFormData(examineBusinessPostListOld, examineGoodsOld, businessPostList)
    /* 数据 */
    state.examineGoods_new = Tool.returnExamineGoods(examineGoodsNew) // 报告信息_新
    state.examineGoods_old = Tool.returnExamineGoods(examineGoodsOld) // 报告信息_旧
    state.examineBusinessPostList_new = examineBusinessPostListNew //    岗位对应比例_新
    state.examineBusinessPostList_old = examineBusinessPostListOld //    岗位对应比例_旧
    state.customMap = customMap //                                       客户信息
    state.formData_new = formData_new //                                 表单数据_新
    state.formData_old = formData_old //                                 表单数据_旧
    state.tableData_new = tableData_new //                               表格：原始数据_新
    state.tableData_old = tableData_old //                               表格：原始数据_旧
    state.storehouse_new = storehouse_new //                             仓库_新
    state.storehouse_old = storehouse_old //                             仓库_旧
    /* 选项 */
    state.peopleList = Tool.peopleList(businessPostList) //              岗位下：人员列表
    state.arrOut = Tool.returnArrOut(wbzrgs) //                          外部
    state.arrIn = Tool.returnArrIn(businessPostList) //                  内部
    state.arrResultType = Tool.returnCate(examineNoQualifyList) //       原因类型
    state.arrHandlingType = Tool.returnYhclfs(yhclfs) //                 处理方式
    state.examineGoodsModify = examineGoodsModify //                     变更说明
    /* change 事件：验货日期 */
    commit('changeTime')
    /** change 事件：责任归属 **/
    commit('changeCheckbox')
  }
  Api({ name, obj, suc, loading: '加载数据中...' })
}

export default Prod
