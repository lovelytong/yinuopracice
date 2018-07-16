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
    <el-dialog
      title="Add User"
      :visible.sync="dialogVisible"
      width="30%"
      :before-close="handleClose"
    >
      <el-form :model="ruleForm" :rules="rules" ref="ruleForm" label-width="80px" class="demo-ruleForm">
        <el-form-item label="Email" prop="email">
          <el-input v-model="ruleForm.email"></el-input>
        </el-form-item>
        <el-form-item label="Username" prop="username">
          <el-input v-model="ruleForm.username"></el-input>
        </el-form-item>
        <el-form-item label="Name" prop="name">
          <el-input v-model="ruleForm.name"></el-input>
        </el-form-item>
        <el-form-item label="Group" prop="group">
          <el-input v-model="ruleForm.group"></el-input>
        </el-form-item>
      </el-form>
      <span slot="footer" class="dialog-footer">
        <el-button @click="resetForm">重 置</el-button>
      <el-button @click="dialogVisible = false">取 消</el-button>
      <el-button type="primary" @click="submitForm">确 定</el-button>
      </span>
    </el-dialog>
    <div class="content-table">
      <div>
        <div class="table-above">
          <div>
            <img src="@/assets/content1.png"/>
          </div>
          <div>
            <el-button type="primary" size="mini" @click="dialogVisible = true">Add User</el-button>
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
      }],
      dialogVisible: false,
      ruleForm: {
        email: '',
        username: '',
        name: '',
        group: ''
      },
      rules: {
        email: [
          {required: true, message: '请输入内容', trigger: 'blur'}
        ],
        username: [
          {required: true, message: '请输入内容', trigger: 'blur'}
        ],
        name: [
          {required: true, message: '请输入内容', trigger: 'blur'}
        ],
        group: [
          {required: true, message: '请输入内容', trigger: 'blur'}
        ]
      }
    }
  },
  methods: {
    submitForm () {
      this.dialogVisible = false;
      this.$refs.ruleForm.validate((valid) => {
        if (valid) {
          alert('submit!');
        } else {
          console.log('error submit!!');
          return false;
        }
      });
    },
    resetForm () {
      console.log(this)
      this.$refs.ruleForm.resetFields();
    },
    handleClose(done) {
      this.$confirm('确认关闭？')
        .then(_ => {
          done();
        })
        .catch(_ => {});
    }
  }
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

  .demo-ruleForm {

  }

</style>
