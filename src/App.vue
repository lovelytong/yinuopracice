<template>
  <div id="app">
    <div class="header">
      <el-row class="header-container">
        <el-col class="header-title" :span="4">
          <div>PROJECT<span style="color: cornflowerblue">BOX</span></div>
        </el-col>
        <el-col :span="12" class="header-title">
          <div></div>
        </el-col>
        <el-col class="header-icon" :span="3">
          <div><i class="el-icon-tickets"></i></div>
          <div><i class="el-icon-message"></i></div>
          <div><i class="el-icon-bell"></i></div>
        </el-col>
        <el-col class="header-admin" :span="3">
          <div><i class="el-icon-tickets"></i></div>
          <div>Project Admin</div>
          <div><i class="el-icon-arrow-down"></i></div>
        </el-col>
      </el-row>
    </div>
    <router-view/>
  </div>
</template>

<script>
export default {
  name: 'App'
}
</script>

<style>
  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    height: 100%;
  }

  * {
    margin: 0;
    padding: 0;
  }

  .header {
    background-color: white;
  }

  .header-container {
    margin: 30px 50px 0 50px;
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
</style>
