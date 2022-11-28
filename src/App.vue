<template>
  <v-app>
    <header>
      <Header/>
    </header>
    <v-main role='presentation' class='main-internal-content' id="main_content" tabindex="-1">
      <v-container class="text-center" :class="{'container--fluid': $vuetify.breakpoint.smAndDown}">
        <router-view/>
      </v-container>
    </v-main>
  </v-app>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import Header from '@/components/Header.vue'

@Component({
  components: {
    Header
  }
})
export default class App extends Vue {


}
</script>
<style lang="scss" scoped>
#app {
  .main-internal-content {
    background-color: #f5f5f5;
    padding: 155px 0 120px 0 !important;
    &:focus{
      outline: 0;
    }
  }
  .hide {
    visibility: hidden;
  }
}
</style>
