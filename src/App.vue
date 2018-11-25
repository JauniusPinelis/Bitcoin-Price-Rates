<template>
  <div id="app">
    <!--<img alt="Vue logo" src="./assets/logo.png"> -->
    <Main />
    <notifications position="top center" group="notification" />
  </div>
</template>

<script>
import Vue from 'vue'
import Notifications from 'vue-notification'
import Main from './components/Main.vue'
import BootstrapVue from 'bootstrap-vue'
import CurrencyDisplay from './components/CurrencyDisplay.vue'

import 'bootstrap/dist/css/bootstrap.css'
import 'bootstrap-vue/dist/bootstrap-vue.css'
import { library } from '@fortawesome/fontawesome-svg-core'
import { faTimesCircle } from '@fortawesome/free-solid-svg-icons'
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome'

Vue.use(BootstrapVue);
Vue.use(Notifications);

library.add(faTimesCircle)

Vue.component('font-awesome-icon', FontAwesomeIcon)
Vue.component('Main', Main)
Vue.component('currency-display', CurrencyDisplay)

export default {
  name: 'app'
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
