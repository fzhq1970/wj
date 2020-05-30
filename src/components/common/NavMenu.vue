<template>
  <el-menu :default-active="'/home'" router mode="horizontal" background-color="white" text-color="#222"
    active-text-color="red">
    <el-menu-item v-for="(item,i) in navList" :key="i" :index="item.name"  style="font-size: 16px;font-weight: bold">
      {{ item.navItem }}
    </el-menu-item>
    <i class="el-icon-switch-button" v-on:click="logout" style="float:right;font-size: 40px;color: #222;padding: 10px"></i>
    <a href="#nowhere" style="color: #222;float: right;padding: 20px;">更多功能</a>
    <i class="el-icon-menu" style="float:right;font-size: 45px;color: #222;padding-top: 8px"></i>
    <span style="position: absolute;padding-top: 20px;right: 35%;font-size: 20px;font-weight: bold">
      测试学习
    </span>
  </el-menu>
</template>

<script>
export default {
  name: 'NavMenu',
  data () {
    return {
      navList: [
        {name: '/home', navItem: '首页'},
        {name: '/user/register', navItem: '用户注册'},
        {name: '/library', navItem: '图书馆'},
        {name: '/admin', navItem: '个人中心'}
      ]
    }
  },
  methods: {
    logout () {
      var _this = this
      this.$axios.get('/logout').then(resp => {
        if (resp.data.code === 200) {
          // 前后端状态保持一致
          _this.$store.commit('logout')
          _this.$router.replace('/login')
        }
      })
    }
  }
}
</script>

<style>
    a{
      text-decoration: none;
    }
    span {
      pointer-events: none;
    }
    .el-icon-switch-button {
      cursor: pointer;
      outline:0;
    }
</style>
