<template>
  <el-row >
    <el-col :span="5">
      <div class="menu-background">
        <el-menu
          default-active="1-1"
          class="el-menu-vertical-demo"
          @open="handleOpen"
          @close="handleClose"
          background-color="#658bb1"
          text-color="#fff"
          active-text-color="#47c5f0">
          <el-menu-item>
            <i class="el-icon-menu"></i>
            <span slot="title">Dashboard</span>
          </el-menu-item>
          <el-menu-item>
            <i class="el-icon-document"></i>
            <span slot="title">Calendar</span>
          </el-menu-item>
          <el-menu-item>
            <i class="el-icon-setting"></i>
            <span slot="title">Tasks</span>
          </el-menu-item>
          <el-menu-item>
            <i class="el-icon-menu"></i>
            <span slot="title">File Manager</span>
          </el-menu-item>
          <el-submenu index="1">
            <template slot="title">
              <i class="el-icon-location"></i>
              <span>Team</span>
            </template>
            <el-menu-item-group>
              <el-menu-item index="1-1">Manage</el-menu-item>
              <el-menu-item index="1-2">Groups</el-menu-item>
            </el-menu-item-group>
          </el-submenu>
          <el-menu-item>
            <i class="el-icon-menu"></i>
            <span slot="title">Time Logger</span>
          </el-menu-item>
          <el-menu-item>
            <i class="el-icon-document"></i>
            <span slot="title">Discuss</span>
          </el-menu-item>
          <el-menu-item>
            <i class="el-icon-setting"></i>
            <span slot="title">Tickets</span>
          </el-menu-item>
          <el-menu-item>
            <i class="el-icon-setting"></i>
            <span slot="title">Accounting</span>
          </el-menu-item>
        </el-menu>
      </div>
    </el-col>
    <el-col :span="19" class="main">
      <div class="white-background margin-50 border-radius-5" style="height: 30px;">
        <el-breadcrumb separator="/">
          <el-breadcrumb-item :to="{ path: '/' }">首页</el-breadcrumb-item>
          <el-breadcrumb-item><a href="/">活动管理</a></el-breadcrumb-item>
          <el-breadcrumb-item>活动列表</el-breadcrumb-item>
          <el-breadcrumb-item>活动详情</el-breadcrumb-item>
        </el-breadcrumb>
      </div>
      <div class="white-background margin-50 border-radius-5">
        <el-table
          :data="tableData"
          border
          style="width: 100%">
          <el-table-column
            prop="date"
            label="日期"
            width="180">
          </el-table-column>
          <el-table-column
            prop="name"
            label="姓名"
            width="180">
          </el-table-column>
          <el-table-column
            prop="address"
            label="地址">
          </el-table-column>
          <el-table-column label="操作">
            <template slot-scope="scope">
              <el-button
                size="mini"
                @click="handleEdit(scope.$index, scope.row)"
                type="warning"
              >Edit
              </el-button>
              <el-button
                size="mini"
                type="danger"
                @click="handleDelete(scope.$index, scope.row)">Romove
              </el-button>
            </template>
          </el-table-column>
        </el-table>
      </div>
    </el-col>
  </el-row>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      tableData: [{
        date: '2016-05-02',
        name: '王小虎',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        date: '2016-05-04',
        name: '王小虎',
        address: '上海市普陀区金沙江路 1517 弄'
      }, {
        date: '2016-05-01',
        name: '王小虎',
        address: '上海市普陀区金沙江路 1519 弄'
      }, {
        date: '2016-05-03',
        name: '王小虎',
        address: '上海市普陀区金沙江路 1516 弄'
      }]
    }
  },
  methods: {
    handleOpen (key, keyPath) {
      console.log(key, keyPath)
    },
    handleClose (key, keyPath) {
      console.log(key, keyPath)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .main {
    background-color: #eeeeee;
    height: 850px;
    padding-left: 50px;
    padding-right: 50px;
  }

  .white-background {
    background-color: white;
  }

  .margin-50 {
    margin-top: 50px;
  }

  .border-radius-5 {
    border-radius: 5px;
  }

  .menu-background {
    background-color: white;
    padding-left: 50px;
  }
  .el-menu-vertical-demo {
    height: 850px;
  }

</style>
