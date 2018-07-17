<template>
  <div class="main">
    <div class="message-box" v-if="boxShow">
      <div><span style="font-weight: bolder">Notice:</span>{{boxMessage}}</div>
    </div>
    <div class="bread-crumb">
      <el-breadcrumb separator="/">
        <el-breadcrumb-item :to="{ path: '/' }">
          <span style="color: #669CCC">MyProject</span>
        </el-breadcrumb-item>
        <el-breadcrumb-item><a href="/">Team Management</a></el-breadcrumb-item>

      </el-breadcrumb>
    </div>
    <el-dialog
      :title="dialogName"
      :visible.sync="dialogVisible"
      width="30%"
      :before-close="handleClose"
    >
      <el-form :model="ruleForm" :rules="rules" ref="ruleForm" label-width="80px" class="demo-ruleForm">
        <el-form-item label="Email" prop="email">
          <el-input v-model.trim="ruleForm.email"></el-input>
        </el-form-item>
        <el-form-item label="Username" prop="username">
          <el-input v-model.trim="ruleForm.username"></el-input>
        </el-form-item>
        <el-form-item label="Name" prop="name">
          <el-input v-model.trim="ruleForm.name"></el-input>
        </el-form-item>
        <el-form-item label="Group" prop="group">
          <el-input v-model.trim="ruleForm.group"></el-input>
        </el-form-item>
      </el-form>
      <span slot="footer" class="dialog-footer">
        <el-button @click="resetForm">RESET</el-button>
      <el-button @click="cancelDialog">CANCEL</el-button>
      <el-button type="primary" @click="submitForm" v-if="submitButton">SUBMIT</el-button>
        <el-button type="primary" @click="updateForm" v-if="updateButton">UPDATE</el-button>
      </span>
    </el-dialog>
    <div class="content-table">
      <div>
        <div class="table-above">
          <div>
            <img src="@/assets/content1.png"/>
          </div>
          <div>
            <el-button type="primary" size="mini" @click="openAddDialog">Add User</el-button>
          </div>
        </div>
        <hr>
        <el-table
          :data="tableData"
          border
          style="width: 100%"
          :header-cell-style="{backgroundColor:'#e7e9ec'}"
          header-row-class-name="test"
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
      dialogName:'',
      editRow: null,
      submitButton: true,
      updateButton: true,
      boxShow: false,
      boxMessage: '',
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
          {required: true, message: 'Please enter!', trigger: 'blur'}
        ],
        username: [
          {required: true, message: 'Please enter!', trigger: 'blur'}
        ],
        name: [
          {required: true, message: 'Please enter!', trigger: 'blur'}
        ],
        group: [
          {required: true, message: 'Please enter!', trigger: 'blur'}
        ]
      }
    }
  },
  methods: {
    handleEdit (index, row) {
      this.ruleForm = row
      this.editRow = index
      this.updateButton = true
      this.submitButton = false
      this.dialogName = 'Update User'
      this.dialogVisible = true
    },
    updateForm: function () {
      this.$refs.ruleForm.validate((valid) => {
        if (valid) {
          this.tableData.splice(this.editRow, 1, this.ruleForm)
          console.log(this.tableData[this.editRow])
          this.boxShow = true
          this.boxMessage = 'update success!!'
        } else {
          this.boxShow = true
          this.boxMessage = 'error submit!!'
        }
      })
      setTimeout(() => {
        this.boxShow = false
      }, 2000)
      this.dialogVisible = false
    },
    handleDelete (index) {
      this.tableData.splice(index, 1)
      this.boxShow = true
      this.boxMessage = 'This team member was deleted from project!'
      setTimeout(() => {
        this.boxShow = false
      }, 2000)
    },
    submitForm: function () {
      // let obj = JSON.parse(JSON.stringify(this.ruleForm))
      let obj = Object.assign({}, this.ruleForm)
      this.$refs.ruleForm.validate((valid) => {
        if (valid) {
          this.tableData.push(obj)
          this.boxShow = true
          this.boxMessage = 'The user was added to project!'
        } else {
          this.boxShow = true
          this.boxMessage = 'error update!!'
        }
        setTimeout(() => {
          this.boxShow = false
        }, 2000)
      })
      this.$refs.ruleForm.resetFields()
      this.dialogVisible = false
    },
    resetForm () {
      this.$refs.ruleForm.resetFields()
      this.ruleForm = {
        email: '',
        username: '',
        name: '',
        group: ''
      }
    },
    handleClose (done) {
      this.$confirm('confirm close？')
        .then(_ => {
          done()
        })
        .catch(_ => {
        })
    },
    cancelDialog () {
      this.$refs.ruleForm.resetFields()
      this.dialogVisible = false
    },
    openAddDialog () {
      this.updateButton = false
      this.submitButton = true
      this.dialogName = 'Add User'
      this.dialogVisible = true
      this.ruleForm = {
        email: '',
        username: '',
        name: '',
        group: ''
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

  .main {
    background-color: #eeeeee;
    height: calc(100vh - 95px);
    overflow: auto;
    padding-left: 50px;
    padding-right: 50px;
    padding-top: 20px;
  }

  .message-box {
    background-color: #dff0d7;
    border-radius: 5px;
    margin-bottom: 30px;
    padding: 20px;
    padding-left: 50px;
    display: flex;
    justify-content: start;
    align-items: center;
    color: #3c783c;
    font-size: 18px;
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
