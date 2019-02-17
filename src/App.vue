<template>
  <div id="app">
    <!-- <img alt="Vue logo" src="./assets/logo.png"> -->
    <br>
    <img :src="app.iconUrl" height="100" width="100">
    <h1>{{app.name}}</h1>
    <p>{{profile.nickname}}こんにちは！</p>
    <button class="btn btn-primary col-xs-12 " @click="getProfile">個人情報</button>
    <br>
    <button class="btn btn-primary col-xs-12 " @click="getAssets">お金を見せてくれ</button>
    <br>
    <button class="btn btn-primary col-xs-12 " @click="donate">投げ銭</button>

    <br>
    <ul>
      <li v-for="a in assets" :key="a.assetsId">
        <img :src="a.iconUrl" height="15" width="15">
        {{a.name}} - {{a.assetId}}
      </li>
    </ul>
  </div>
</template>

<script>
import coinview from '@coinjinja/coinview-sdk'

export default {
  name: 'app',
  data() {
    return {
      app: {},
      profile: {},
      assets: [],
    }
  },
  methods: {
    async getProfile() {
      this.profile = await coinview.user.profile()
      alert(1)
    },
    async donate() {
      const payload = {
        assetId: '07065d64-fd33-39b5-b275-9a2cc4806ef4',
        amount: 1,
        description: '投げ銭'
      }
      const payment = await coinview.payment.create(payload)
    },
    async getAssets() {
      this.assets = await coinview.user.assets()
      alert(2)
    }
  },
  async mounted() {
    await coinview.init('7Jqg63Em')
    this.app = await coinview.app()
  }
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
