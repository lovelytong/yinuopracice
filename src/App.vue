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
            <div v-for="item in menuData1" :key="item.id">
              <div class="main-item">
                <div>
                  <i class="el-icon-edit"></i>
                  {{item.text}}
                </div>
                <div>+</div>
              </div>
            </div>
            <div style="background-color: #445C74;color:white;margin:10px 0;">
              <div class="team-title" @click="toggleMenu">
                <div>
                  <i class="el-icon-edit"></i>
                  Team
                </div>
                <div>+</div>
              </div>
              <div class="team-content" v-if="menushow">
                <div class="team-content-li" style="color: #56C7F2">
                  <i class="el-icon-arrow-right"></i>&#8195;
                  Manage</div>
                <div class="team-content-li" style="padding-bottom: 15px">
                  <i class="el-icon-arrow-right"></i>&#8195;
                  Groups
                </div>
              </div>
            </div>
            <div v-for="item in menuData2" :key="item.id">
              <div class="main-item">
                <div>
                  <div>
                    <i class="el-icon-edit"></i>
                    {{item.text}}
                  </div>

                </div>
                <div>+</div>
              </div>

            </div>

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
      menushow: true,
      menuData1: [
        {
          id: 0,
          text: 'Dashboard'
        },
        {
          id: 1,
          text: 'Calendar'
        },
        {
          id: 2,
          text: 'Tasks'
        },
        {
          id: 3,
          text: 'File Manager'
        }
      ],
      menuData2: [
        {
          id: 4,
          text: 'Time Logger'
        },
        {
          id: 5,
          text: 'Discuss'
        },
        {
          id: 6,
          text: 'Tickets'
        },
        {
          id: 7,
          text: 'Accounting'
        }
      ]
    }
  },
  methods: {
    toggleMenu () {
      this.menushow = !this.menushow
    }
  },
  mounted () {

  }
}
</script>

<style>
  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    user-select: none;
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
    cursor: pointer;
  }

  .header-icon {
    display: flex;
    justify-content: space-around;
    align-items: center;
    height: 60px;
    border-right: 2px solid #eeeeee;
    font-size: 30px;
    cursor: pointer;
  }

  .header-admin {
    display: flex;
    justify-content: space-around;
    align-items: center;
    height: 60px;
    cursor: pointer;
  }

  .menu {
    height: calc(100vh - 90px);
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

  .main-item {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 20px;
    color: white;
    font-size: 16px;
    font-weight: bolder;
  }
  .team-title {
    display: flex;
    justify-content: space-between;
    padding: 10px 20px 10px;
    font-weight: bolder;
    cursor: pointer;
  }
  .team-content{
    width: 100%;
    background-color:#587899 ;
    font-weight: bolder;
    cursor: pointer;
  }
  .team-content-li{
    padding:15px 10px 0 40px;
  }

</style>
