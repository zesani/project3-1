<template lang="html">
  <div class="">
    <div class="" v-for="list in listplay">
      {{list}}
    </div>
    <button type="button" name="button" @click="de"></button>
  </div>
</template>

<script>
import firebase from 'firebase'
var config = {
  apiKey: 'AIzaSyDzZeuk5iAFxBciQ1mDErvqe1UZF15Rf5c',
  authDomain: 'sorndev.firebaseapp.com',
  databaseURL: 'https://sorndev.firebaseio.com',
  storageBucket: 'sorndev.appspot.com',
  messagingSenderId: '857410261779'
}
firebase.initializeApp(config)
var Listplay = firebase.database().ref('listplay')
export default {
  data () {
    return {
      listplay: []
    }
  },
  mounted () {
    var vm = this
    Listplay.on('child_added', function (data) {
      var item = data.val()
      item.id = data.key
      vm.listplay.push(item)
    })
  },
  methods: {
    de () {
      firebase.database().ref('listplay/0').remove()
    }
  }
}
</script>

<style lang="css">
</style>
