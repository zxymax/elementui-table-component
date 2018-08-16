<template>
<div>
<m-select :myOptions="selectOptions" />
<m-select :myOptions="selectOptions2" />
  <el-table
    :data="tableData"
    style="width: 100%">
    <el-table-column
    v-for="(item, index) in colunms" :key="index"
      :label="item.label"
      :width="item.width  ">
      <template slot-scope="scope">
         <m-select  v-if="scope.row.seen==true && item.type=='select'" :myOptions="selectOptions" />
         <el-input v-else-if="scope.row.seen==true &&  item.type=='text'" v-model="scope.row[item.key]"

         ></el-input>  

        <span style="margin-left: 10px"  v-else>{{ scope.row[item.key] }}</span>
      </template>
    </el-table-column>

    <el-table-column label="操作">
      <template slot-scope="scope">
        <el-button
          size="mini"
          @click="handleEdit(scope.$index, scope.row)">编辑</el-button>
        <el-button
          size="mini"
          type="danger"
           @click.native.prevent="deleteRow(scope.$index, tableData)">删除</el-button>
      </template>
    </el-table-column>
  </el-table>
  </div>
</template>

<script>
  import MSelect from './Select'
  export default {
    components: {
      MSelect
    },
    data() {
      return {
        colunms: [
          { label: '日期', width: '120', key: 'date', type: 'text' },
          { label: '姓名', width: '220', key: 'name', type: 'select' },
          { label: '地址', width: '330', key: 'address', type: 'text' }
        ],
        tableData: [{
          seen: false,
          date: '2016-05-02',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄'
        }, {
          seen: false,
          date: '2016-05-04',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1517 弄'
        }, {
          seen: false,
          date: '2016-05-01',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1519 弄'
        }, {
          seen: false,
          date: '2016-05-03',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1516 弄'
        }],
        selectOptions2: {
          defaultV: '选项3',
          options: [{
            value: '选项1',
            label: '黄金糕'
          }, {
            value: '选项2',
            label: '双皮奶'
          }, {
            value: '选项3',
            label: '蚵仔煎'
          }, {
            value: '选项4',
            label: '龙须面'
          }, {
            value: '选项5',
            label: '北京烤鸭'
          }]
        },
        selectOptions:{
          defaultV: 'beijing',
          options: [{
            value: 'beijing',
            label: '北京'
          }, {
            value: 'tianjin',
            label: '天津'
          }, {
            value: 'xian',
            label: '西安'
          }, {
            value: 'shanghai',
            label: '上海'
          }, {
            value: 'guangzhou',
            label: '广州'
          }]
        } 
       

      }
      
    },
    methods: {   
      handleEdit(index, row) {
        row.seen = true
      },
      deleteRow(index, rows) {
        rows.splice(index, 1);
      },
      loseFcous(index, row) {
        row.seen=false;
      },
      getColumns() {
        let columnsArr = []   
        for(let key of Object.keys(this.tableData[0])){
          columnsArr.push(key)
        }
        this.columns =  columnsArr.filter(item=>{
          return item != 'seen'
        })
       
      }
    },
    mounted() {
      console.log(this.tableData.length)
      this.getColumns()
    }
  }
</script>