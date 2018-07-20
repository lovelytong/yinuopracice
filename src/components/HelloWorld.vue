<template>
  <div>
    <!--提示框，正常情况下隐藏，提交表单成功或者失败给出提示，三秒后再次隐藏,带有淡出的动画效果-->
    <transition name="fade">
      <div class="message-box" v-if="boxShow">
        <div><span style="font-weight: bolder">Notice:</span>{{boxMessage}}</div>
      </div>
    </transition>
    <!--模态框，里面是表格数据增加和修改的表单，点击新增和修改的时候出现-->
    <el-dialog
      :title="dialogName"
      :visible.sync="dialogVisible"
      width="30%"
      :before-close="handleClose"
    >
      <el-form :model="ruleForm" :rules="rules" ref="ruleForm" label-width="80px" class="demo-ruleForm">
        <el-form-item label="Email" prop="email">
          <el-input v-model.trim="ruleForm.email" style="width: 90%;"></el-input>
        </el-form-item>
        <el-form-item label="Username" prop="username">
          <el-input v-model.trim="ruleForm.username" style="width: 90%;"></el-input>
        </el-form-item>
        <el-form-item label="Name" prop="name">
          <el-input v-model.trim="ruleForm.name" style="width: 90%;"></el-input>
        </el-form-item>
        <el-form-item label="Group" prop="group">
          <el-select v-model.trim="ruleForm.group" placeholder="choose group" style="width: 90%;">
            <el-option label="Admin" value="Admin"></el-option>
            <el-option label="customer" value="customer"></el-option>
          </el-select>
        </el-form-item>
      </el-form>
      <span slot="footer" class="dialog-footer">
        <el-button @click="resetForm" size="mini" v-if="submitButton">RESET</el-button>
      <el-button @click="cancelDialog" size="mini">CANCEL</el-button>
      <el-button type="primary" @click="submitForm" v-if="submitButton" size="mini">SUBMIT</el-button>
        <el-button type="primary" @click="updateForm" v-if="updateButton" size="mini">UPDATE</el-button>
      </span>
    </el-dialog>
    <!--面包屑导航部分-->
    <div class="bread-crumb">
      <el-breadcrumb separator="/">
        <el-breadcrumb-item :to="{ path: '/' }">
          <span style="color: #669CCC">MyProject</span>
        </el-breadcrumb-item>
        <el-breadcrumb-item><a href="/">Team Management</a></el-breadcrumb-item>
      </el-breadcrumb>
    </div>
    <!--表格部分-->
    <div class="content-table">
      <div>
        <div class="table-above">
          <div>
            <img src="@/assets/content1.png"/>
          </div>
          <el-input placeholder="search by username" v-model="searchItem" class="input-with-select" style="width: 30%"
                    @keyup.native.enter="search">
            <el-button slot="append" icon="el-icon-search" @click="search"></el-button>
          </el-input>
          <div>
            <el-button type="primary" size="mini" @click="openAddDialog">Add User</el-button>
          </div>
        </div>
        <hr>
        <el-table
          :data="tableData"
          border
          style="width: 100%"
          :header-cell-style="{backgroundColor:'#F0F0F0'}"
          header-row-class-name="test"
        >
          <el-table-column
            prop="email"
            label="Email"
          >
          </el-table-column>
          <el-table-column
            label="Username">
            <template slot-scope="scope">
              <p v-html="scope.row.username" class="father"></p>
            </template>
          </el-table-column>
          <el-table-column
            prop="name"
            label="Name">
          </el-table-column>
          <el-table-column
            prop="group"
            label="Group">
          </el-table-column>
          <el-table-column
            prop="date"
            label="Date">
          </el-table-column>
          <el-table-column label="Options" width="180">
            <template slot-scope="scope">
              <el-button
                size="mini"
                type="warning"
                @click="handleEdit(scope.$index, scope.row)">Edit
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
    </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data: function () {
    var checkEmail = (rule, value, callback) => {
      const testEmail = /^[a-z0-9]+([._\\-]*[a-z0-9])*@([a-z0-9]+[-a-z0-9]*[a-z0-9]+.){1,63}[a-z0-9]+$/
      if (!value) {
        return callback(new Error('邮件不能为空'))
      }
      if (testEmail.test(value)
      ) {
        return callback()
      } else {
        return callback(new Error('请输入正确格式的邮箱'))
      }
    }
    return {
      searchItem: null,
      creatDate: '',
      // 控制模态框的变量
      dialogVisible: false,
      dialogName: '',
      editRow: null,
      submitButton: true,
      updateButton: true,
      // 消息提示框变量
      boxShow: false,
      boxMessage: '',
      // 模态框双向绑定数据
      ruleForm: {
        email: '',
        username: '',
        name: '',
        group: ''
      },
      // 表格数据
      tableData: [{
        email: 'admin@admin.com',
        username: 'admin',
        name: 'Project Admin',
        group: 'Admin',
        date: '2018年07月15日'
      }, {
        email: 'test@test.com',
        username: 'test',
        name: 'test test2',
        group: 'Admin',
        date: '2018年07月15日'
      }, {
        email: 'test@test.com',
        username: 'test',
        name: 'test test2',
        group: 'Admin',
        date: '2018年07月15日'
      }, {
        email: 'test@test.com',
        username: 'test',
        name: 'test test2',
        group: 'Admin',
        date: '2018年07月15日'
      }],
      // 表单验证
      rules: {
        email: [
          {required: true, validator: checkEmail, trigger: 'blur'}
        ],
        username: [
          {required: true, message: 'Please enter!', trigger: 'blur'}
        ],
        name: [
          {required: true, message: 'Please enter!', trigger: 'blur'}
        ],
        group: [
          {required: true, message: 'Please choose!', trigger: 'change'}
        ]
      }
    }
  },
  computed: {

  },
  methods: {
    search () {
      let arr = []
      for (let i = 0, l = this.tableData.length; i < l; i++) {
        this.tableData[i].username = this.tableData[i].username.replace(/<span>|<\/span>/g, '')
        if (this.tableData[i].username.indexOf(this.searchItem) >= 0) {
          arr.push(i)
        }
      }
      if (arr.length > 0) {
        // const strSpanstart = '<span style="color:red">', strSpanend = '</span>'
        // i.replace(/<[^<>]+p>/ig,"");这样写

        // const exp = '/(<span>*) | (<\/span>*$)/g'
        // let reg1 = new RegExp(strSpanstart, 'g')
        // let reg2 = new RegExp(strSpanend, 'g')
        let reg = new RegExp(this.searchItem, 'g')
        for (let index of arr) {
          // this.tableData[index].username = this.tableData[index].username.replace(/<span>|<\/span>/g, '')
          // this.tableData[index].username = this.tableData[index].username.replace(reg1, '')
          // this.tableData[index].username = this.tableData[index].username.replace(reg2, '')
          this.tableData[index].username = this.tableData[index].username.replace(reg, '<span>' + this.searchItem + '</span>')
        }
      }
    },

    dateString: function (arr) {
      let formatDate = arr.split('/')
      for (let i = 0, l = formatDate.length; i < l; i++) {
        let thisFormDate = formatDate[i]
        if (thisFormDate.length < 2) {
          formatDate[i] = '0' + thisFormDate
        }
      }
      return formatDate[0] + '年' + formatDate[1] + '月' + formatDate[2] + '日'
    },
    // 点击新增按钮
    openAddDialog () {
      this.updateButton = false
      this.submitButton = true
      this.dialogName = 'Add User'
      this.dialogVisible = true
      // this.ruleForm = {
      //   email: '',
      //   username: '',
      //   name: '',
      //   group: '',
      //   date: ''
      // }
      this.$refs.ruleForm.resetFields()
    },
    // 点击编辑按钮
    handleEdit (index, row) {
      this.ruleForm = Object.assign({}, row)
      this.editRow = index
      this.updateButton = true
      this.submitButton = false
      this.dialogName = 'Update User'
      this.dialogVisible = true
      this.$refs.ruleForm.resetFields()
    },
    // 点击删除按钮
    handleDelete (index) {
      this.tableData.splice(index, 1)
      this.boxShow = true
      this.boxMessage = 'This team member was deleted from project!'
      setTimeout(() => {
        this.boxShow = false
      }, 2000)
    },
    // 点击模态框里的update按钮
    updateForm: function () {
      let isValid = false
      this.$refs.ruleForm.validate((valid) => {
        if (valid) {
          isValid = true
          this.tableData.splice(this.editRow, 1, JSON.parse(JSON.stringify(this.ruleForm)))
          this.boxShow = true
          this.boxMessage = 'update success!!'
        } else {
          this.boxShow = true
          this.boxMessage = 'error update!!'
        }
      })
      setTimeout(() => {
        this.boxShow = false
      }, 3000)
      if (!isValid) {
        return
      }
      this.dialogVisible = false
    },
    // 点击模态框里的submit按钮
    submitForm: function () {
      this.creatTime = new Date().toLocaleDateString()
      let isValid = false
      this.ruleForm.date = this.dateString(this.creatTime)
      let obj = Object.assign({}, this.ruleForm)
      this.$refs.ruleForm.validate((valid) => {
        if (valid) {
          isValid = true
          this.tableData.unshift(obj)
          this.boxShow = true
          this.boxMessage = 'The user was added to project!'
        } else {
          this.boxShow = true
          this.boxMessage = 'error add!!'
        }
        setTimeout(() => {
          this.boxShow = false
        }, 3000)
      })
      if (!isValid) {
        return
      }
      this.dialogVisible = false
    },
    // 表单重置
    resetForm () {
      this.$refs.ruleForm.resetFields()
      this.ruleForm = {
        email: '',
        username: '',
        name: '',
        group: ''
      }
    },
    // 点击模态框取消按钮
    cancelDialog () {
      this.dialogVisible = false
    },

    // 点击模态框的关闭按钮
    handleClose (done) {
      this.$confirm('confirm close？')
        .then(_ => {
          done()
        })
        .catch(_ => {
        })
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
  .father span {
    color:red
  }
  .message-box {
    border-radius: 5px;
    margin-bottom: 30px;
    padding: 20px 20px 20px 50px;
    display: flex;
    justify-content: start;
    align-items: center;
    color: #3c783c;
    font-size: 18px;
    background-color: #dff0d7;
  }

  .fade-enter-active, .fade-leave-active {
    transition: opacity .5s;
  }

  .fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */
  {
    opacity: 0;
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

  el-table--border td, .el-table--border th, .el-table__body-wrapper .el-table--border.is-scrolling-left ~ .el-table__fixed {
    border-right: 1px solid #e0e0e0;
  }

</style>
