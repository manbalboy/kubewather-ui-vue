<template>
  <div class="sidebar" :data="backgroundColor">
    <div ref="sidebarScrollArea" class="sidebar-wrapper">
      <div class="logo">
        <a href="#" class="simple-text logo-mini" @click.prevent="$sidebar.toggleMinimize()">
          <img :src="logo" alt="app-logo" />
        </a>
        <a class="simple-text logo-normal">
          {{ title }}
        </a>
      </div>
      <slot></slot>
      <ul class="nav">
        <slot name="links">
          <SidebarItem v-for="(link, index) in sidebarLinks" :key="link.name + index" :link="link">
            <SidebarItem v-for="(subLink, index) in link.children" :key="subLink.name + index" :link="subLink">
            </SidebarItem>
          </SidebarItem>
        </slot>
      </ul>
    </div>
  </div>
</template>
<script>
  export default {
    name: 'Sidebar',
    provide() {
      return {
        autoClose: this.autoClose,
      };
    },
    props: {
      title: {
        type: String,
        default: 'Creative Tim',
        description: 'Sidebar title',
      },
      shortTitle: {
        type: String,
        default: 'CT',
        description: 'Sidebar short title',
      },
      logo: {
        type: String,
        default: 'http://demos.creative-tim.com/nuxt-black-dashboard-pro/img/icon-nuxt.svg',
        description: 'Sidebar app logo',
      },
      backgroundColor: {
        type: String,
        default: 'vue',
        validator: value => {
          const acceptedValues = ['', 'vue', 'blue', 'green', 'orange', 'red', 'primary'];
          return acceptedValues.includes(value);
        },
        description: 'Sidebar background color (vue|blue|green|orange|red|primary)',
      },
      sidebarLinks: {
        type: Array,
        default: () => [],
        description: "List of sidebar links as an array if you don't want to use components for these.",
      },
      autoClose: {
        type: Boolean,
        default: true,
        description: 'Whether sidebar should autoclose on mobile when clicking an item',
      },
    },
    beforeDestroy() {
      if (this.$sidebar.showSidebar) {
        this.$sidebar.showSidebar = false;
      }
    },
    methods: {
      minimizeSidebar() {
        if (this.$sidebar) {
          this.$sidebar.toggleMinimize();
        }
      },
    },
  };
</script>
<style>
  @media (min-width: 992px) {
    .navbar-search-form-mobile,
    .nav-mobile-menu {
      display: none;
    }
  }
</style>
