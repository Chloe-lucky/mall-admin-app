<template>
  <div class="silder-nav">
    <a-button
      type="primary"
      @click="toggleCollapsed"
    >
      <a-icon :type="$store.state.collapsed ? 'menu-unfold' : 'menu-fold'" />
    </a-button>
    <div class="breadcrumb">
      <a-breadcrumb v-if="currentRoutes.length > 1">
        <a-breadcrumb-item>
          {{currentRoutes[0] ? currentRoutes[0].meta.title : ''}}
        </a-breadcrumb-item>
        <a-breadcrumb-item>
          <router-link :to="{name:currentRoutes[1].name}">
          {{currentRoutes[1] ? currentRoutes[1].meta.title : ''}}
          </router-link>
          </a-breadcrumb-item>
      </a-breadcrumb>
    </div>
    <ul class="user-info">
      <li class="user-name">
        {{$store.state.user.username}}
        <a-icon type="down" />
      </li>
      <li class="login-out" @click="logout">退出</li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      currentRoutes: this.$router.currentRoute.matched,
    };
  },
  watch: {
    $route() {
      this.currentRoutes = this.$router.currentRoute.matched;
    },
  },
  methods: {
    toggleCollapsed() {
      this.$store.dispatch('changeCollapsed');
    },
    logout() {
      this.$store.dispatch('logout');
      this.$router.push({
        name: 'Login',
      });
    },
  },
};
</script>

<style lang='less'>
.user-info{
  position: fixed;
  right: 0;
  top: 0;
}
// .user-info:hover{
//     margin-top: -10px;
//   }
</style>
