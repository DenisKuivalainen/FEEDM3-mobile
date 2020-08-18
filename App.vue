<template>
  <view class="container">
    <Head />
    <Main />
  </view>
</template>

<script>
import Head from './src/Head'
import Main from './src/Main'

export default {
  name: 'App',
  components: {
    Head,
    Main
  }
}
</script>

<style>
.container {
  flex: 1;
  padding-top:25px;
  margin: 5;
}
</style>
