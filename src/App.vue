<template>
  <div id="app">
    <!--顶层菜单,响应式布局-->
    <div class="header">
      <el-row class="header-container">
        <el-col class="header-title" :lg="4" :md="4" :sm="4" :xs="4">
          <div>PROJECT<span style="color: #658bb1">BOX</span></div>
        </el-col>
        <el-col :lg="13" :md="8" :sm="8" :xs="8" class="header-title">
          <div></div>
        </el-col>
        <el-col class="header-icon" :lg="3" :md="6" :sm="6" :xs="6">
          <img src="@/assets/header1.png">
        </el-col>
        <el-col class="header-admin" :lg="4" :md="6" :sm="6" :xs="6">
          <img src="@/assets/header2.png">
        </el-col>
      </el-row>
    </div>
    <!--左侧菜单-->
    <el-row>
      <el-col :span="4" style="min-width: 300px;">
        <div class="menu-background">
          <div class="menu">
            <div v-for="item in menuData1" :key="item.id">
              <div class="main-item">
                <div>
                  <i class="el-icon-edit"></i>&#8195;
                  {{item.text}}
                </div>
                <div>+</div>
              </div>
            </div>
            <div>
              <div class="team-title" @click="menuShow = !menuShow" v-bind:class="{ selectcolor: menuShow }">
                <div>
                  <i class="el-icon-edit"></i>&#8195;
                  Team
                </div>
                <div>+</div>
              </div>
              <div class="team-content" v-if="menuShow">
                <div class="team-content-li" style="color: #56C7F2;margin-bottom: 10px">
                  <i class="el-icon-arrow-right"></i>&#8195;
                  Manage
                </div>
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
                    <i class="el-icon-edit"></i>&#8195;
                    {{item.text}}
                  </div>
                </div>
                <div>+</div>
              </div>

            </div>

          </div>
        </div>
      </el-col>
      <el-col :span="20" class="main">
        <!--主体内容部分，路由动态显示-->
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
      // 控制Team子菜单的展开和收缩
      menuShow: true,

      // 左侧菜单数据
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
  }
}
</script>

<style>
  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    user-select: none;
    min-width: 1024px;
    height: calc(100vh - 10px);
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
    background-color: #658bb1;
    padding-top: 10px;
    height: calc(100vh - 80px);
  }

  .menu-background {
    background-color: white;
    padding-left: 50px;
  }

  .main-item {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 10px 20px;
    color: white;
    font-size: 16px;
    font-weight: bolder;
    cursor: pointer;
  }

  .main-item:hover {
    background-color: #445C74;
  }

  .team-title {
    display: flex;
    justify-content: space-between;
    padding: 11px 20px;
    font-weight: bolder;
    cursor: pointer;
    height: 20px;
    color: white;
  }

  .team-title:hover {
    background-color: #445C74;
  }

  .selectcolor {
    background-color: #445C74;
  }

  .team-content {
    background-color: #587899;
    font-weight: bolder;
    cursor: pointer;
    color: white;
  }

  .team-content-li {
    padding: 15px 10px 0 40px;
  }

  .main {
    background-color: #eeeeee;
    overflow: auto;
    padding-left: 50px;
    padding-right: 50px;
    padding-top: 20px;
    max-width: calc(100% - 300px);
    height: calc(100vh - 70px);
  }

</style>
