<template>
  <div class="div--wrapper--shell">
    <div class="pri-app-header text-center pt-2">
      <h1 class="h1-telecom--heading pl-10 ml-10">Blakes Website</h1>
    </div>
    <v-app-bar id="header_telecom" app color="#ffffff" height="90px">
      <v-toolbar-title>
        <span class="version text-right">{{ version }}</span>
      </v-toolbar-title>
      <v-spacer/>
      <!-- Large Screen -->
      <template v-if="$vuetify.breakpoint.lgAndUp">
        <div class="hidden-md-and-down pt-4 full--height">
          <v-btn v-for="(link, index) in menuItems" :key="index" :class="{'active-route' : link.routeName === $route.name}"
                 class="nav-link full--height" text href="javascript:void(0)" @click="navigate(link.routeName)">
            <v-icon size="20" class="pr-2">{{ link.icon }} </v-icon>
            <span class="font-size--18">{{ link.linkName }}</span>
          </v-btn>
        </div>
        <v-spacer/>
      </template>
      <!--Tablet/Mobile Screen -->
      <template v-else>
        <v-menu
          content-class="mobile-first-menu"
          left
          bottom
        >
          <template v-slot:activator="{ on }">
            <v-btn icon v-on="on" class="hidden-lg-and-up">
              <v-icon>mdi-menu</v-icon>
            </v-btn>
          </template>
          <v-list dense>
            <v-list-item-group
              v-model="selectedItem"
              color="primary"
            >
              <v-list-item v-for="(link, index) in menuItems" :key="index" link @click="navigate(link.routeName)">
                <v-list-item-icon>
                  <v-icon v-text="link.icon"/>
                </v-list-item-icon>
                <v-list-item-content>
                  <v-list-item-title v-text="link.linkName"/>
                </v-list-item-content>
              </v-list-item>
            </v-list-item-group>
          </v-list>
        </v-menu>
      </template>
    </v-app-bar>
  </div>
</template>
<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import { RouteLink } from './types'

@Component
export default class Header extends Vue {
  version = '1.0.0';
  selectedItem = 0;

  protected menuItems: Array<RouteLink> = [
    { linkName: 'Home', routeName: 'Home', icon: 'mdi-view-dashboard' },
    { linkName: 'About', routeName: 'About', icon: 'mdi-information' }
  ];

  navigate(route: string) {
    if (this.$route.name === route) return;
    this.$router.push({ name: route });
  }

  goToLdap() {
    window.open('www.google.com', '_blank')!.focus();
  }
}
</script>

<style lang="scss">
  .v-app-bar.v-app-bar--fixed{
    top: 65px !important;
  }
  .pri-app-header {
    position: fixed;
    height: 65px;
    width: 100%;
    text-align: center;
    background: #073963;
    color: white;
    box-shadow: 0 3px 2px #b8b8b8;
    z-index: 6;
  }
  #header_telecom {
    box-shadow: none;
    .v-btn.nav-link {
      color: #352c2c;
      font-size: 14px;
      padding: 0 18px;
      width: auto;
      &.active-route {
        color: #073963;
        span.v-btn__content{
          border-bottom: solid 3px #073963;
        }
      }
    }
    span.version {
      width: 100%;
      display: inline-block;
      font-size: 16px;
      color: #6d6467;
    }
  }

  .mobile-first-menu {
    left: auto !important;
    right: 0 !important;
  }
  .v-list-item__title{
    overflow: visible !important;
  }
</style>