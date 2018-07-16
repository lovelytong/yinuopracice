<template>
  <div class="main">
    <div class="bread-crumb">
      <el-breadcrumb separator="/">
        <el-breadcrumb-item :to="{ path: '/' }">
          <span style="color: #669CCC">MyProject</span>
        </el-breadcrumb-item>
        <el-breadcrumb-item><a href="/">Team Management</a></el-breadcrumb-item>

      </el-breadcrumb>
    </div>
    <div class="content-table">
      <div>
        <div class="table-above">
          <div>
            <img src="@/assets/content1.png"/>
          </div>
          <div>
            <el-button type="primary" size="mini">Add User</el-button>
          </div>
        </div>
        <hr>
        <el-table
          :data="tableData"
          border
          style="width: 100%"
          :header-cell-style="{backgroundColor:'#e7e9ec'}"
        >
          <el-table-column
            prop="email"
            label="Email"
            width="180">
          </el-table-column>
          <el-table-column
            prop="username"
            label="Username"
            width="180">
          </el-table-column>
          <el-table-column
            prop="name"
            label="Name">
          </el-table-column>
          <el-table-column
            prop="group"
            label="Group">
          </el-table-column>
          <el-table-column label="Options">
            <template slot-scope="scope">
              <el-button
                size="mini"
                type="warning"
                @click="handleEdit(scope.$index, scope.row)">编辑
              </el-button>
              <el-button
                size="mini"
                type="danger"
                @click="handleDelete(scope.$index, scope.row)">删除
              </el-button>
            </template>
          </el-table-column>
        </el-table>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      tableData: [{
        email: 'admin@admin.com',
        username: 'admin',
        name: 'Project Admin',
        group: 'Admin'
      }, {
        email: 'test@test.com',
        username: 'test',
        name: 'test test2',
        group: 'Admin'
      }]
    }
  },
  methods: {}
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

  .main {
    background-color: #eeeeee;
    height: 680px;
    padding-left: 50px;
    padding-right: 50px;
    padding-top: 50px;
  }

  .bread-crumb {
    background-color: white;
    border-radius: 5px;
    margin-bottom: 30px;
    padding: 20px;
  }

  .content-table {
    border-radius: 5px;
    background-color: white;
    padding: 20px;
  }

  hr {
    border-top: 2px solid #e7e9ec;
    margin-bottom: 15px;
  }

  .table-above {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

</style>
