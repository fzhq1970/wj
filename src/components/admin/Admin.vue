<template>
  <el-menu :default-active="'/home'" router mode="horizontal" background-color="white" text-color="#222"
    active-text-color="red">
    <el-menu-item v-for="(item,i) in navList" :key="i" :index="item.name"  style="font-size: 16px;font-weight: bold">
      {{ item.nameZh }}
    </el-menu-item>
    <a href="#nowhere" style="color: #222;float: right;padding: 20px;">更多功能</a>
    <i class="el-icon-menu" style="float:right;font-size: 45px;color: #222;padding-top: 8px"></i>
    <span style="position: absolute;padding-top: 20px;right: 35%;font-size: 20px;font-weight: bold">
      测试学习
    </span>
  </el-menu>
</template>

<script>
export default {
  name: 'Admin',
  data () {
    return {
      navList: [
      ]
    }
  },
  mounted: function () {
    this.loadMenus()
  },
  methods: {
    loadMenus () {
      var _this = this
      this.$axios.get('/menu/menus').then(resp => {
        if (resp.data.code === 200) {
          _this.navList = resp.data.data
          console.log('navList = ' + _this.navList)
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
