<template>
  <footer class="footer__container">
    {{message}}
    <button v-on:click="showFooterMessage">Show Massage</button>
  </footer>
</template>

<script lang="ts">
import {Component, Vue} from 'vue-property-decorator';

@Component
export default class AppFooter extends Vue{
  showFooterMessage(){
    console.log('this is footer massage');
  }
  message = "Sox Shoppng App"
}

</script>

<style lang="scss" scoped>
.footer__container{
  margin-top: 20px;
  padding: 10px;
  background-color: #2c3e50;
  color: white;
}

</style>
