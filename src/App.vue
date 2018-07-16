<template>
  <div id="app">
    <div class="header">
      <el-row class="header-container">
        <el-col class="header-title" :span="4">
          <div>PROJECT<span style="color: cornflowerblue">BOX</span></div>
        </el-col>
        <el-col :span="14" class="header-title">
          <div></div>
        </el-col>
        <el-col class="header-icon" :span="3">
          <img src="@/assets/header1.png">
        </el-col>
        <el-col class="header-admin" :span="3">
          <img src="@/assets/header2.png">
        </el-col>
      </el-row>
    </div>
    <el-row>
      <el-col :span="5">
        <div class="menu-background">
          <div class="menu">
            <ul>
              <li v-for="item in menuData1">
                <div class="main-item">
                  <div>
                    <i class="el-icon-edit"></i>
                    {{item.text}}
                  </div>
                  <div>+</div>
                </div>

              </li>
              <div style="background-color: #445C74;color:white;">
                <div class="team-title">
                  <div>
                    <i class="el-icon-edit"></i>
                    Team
                  </div>
                  <div>+</div>
                </div>
                <div class="team-content">
                  <div class="team-content-li" style="color: #56C7F2">
                    <i class="el-icon-arrow-right"></i>&#8195;
                    Manage</div>
                  <div class="team-content-li" style="padding-bottom: 15px">
                    <i class="el-icon-arrow-right"></i>&#8195;
                    Groups
                  </div>
                </div>
              </div>
              <li v-for="item in menuData2">
                <div class="main-item">
                  <div>
                    <div>
                      <i class="el-icon-edit"></i>
                      {{item.text}}
                    </div>

                  </div>
                  <div>+</div>
                </div>

              </li>
            </ul>
          </div>
        </div>
      </el-col>
      <el-col :span="19" class="main">
        <router-view/>
      </el-col>
    </el-row>
  </div>
</template>

<script>
export default {
  name: 'App',
  data: function () {
    return {
      menuData1: [
        {
          text: 'Dashboard'
        },
        {
          text: 'Calendar'
        },
        {
          text: 'Tasks'
        },
        {
          text: 'File Manager'
        }
      ],
      menuData2: [
        {
          text: 'Time Logger'
        },
        {
          text: 'Discuss'
        },
        {
          text: 'Tickets'
        },
        {
          text: 'Accounting'
        }
      ]
    }
  }
}
</script>

<style>
  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
  }

  * {
    margin: 0;
    padding: 0;
  }

  .header {
    background-color: white;
  }

  .header-container {
    margin: 10px 50px 0 50px;
  }

  .header-title {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 60px;
    border-right: 2px solid #eeeeee;
  }

  .header-icon {
    display: flex;
    justify-content: space-around;
    align-items: center;
    height: 60px;
    border-right: 2px solid #eeeeee;
    font-size: 30px;
  }

  .header-admin {
    display: flex;
    justify-content: space-around;
    align-items: center;
    height: 60px;
  }

  .menu {
    height: 700px;
    background-color: #658bb1;
    padding-top: 15px;
  }

  .menu-background {
    background-color: white;
    padding-left: 50px;
  }

  .el-table thead {
    background-color: red;
  }

  .menu ul {
    list-style-type : none;
  }

  .menu li {
    color: white;
    font-size: 16px;
    font-weight: bolder;
    margin: 20px;

  }

  .main-item {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  .team-title {
    display: flex;
    justify-content: space-between;
    padding: 10px 20px 10px;
    font-weight: bolder;
  }
  .team-content{
    width: 100%;
    background-color:#587899 ;
    font-weight: bolder;
  }
  .team-content-li{
    padding:15px 10px 0 40px;
  }

</style>
