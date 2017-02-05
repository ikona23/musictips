<template>
  <div id="app" class="container">
    <div class="page-header">
        <h1> vue2</h1>
          </div>
<div class="panel panel-default">
  <div class="panel-heading">
    <h3>Add Song</h3>
  </div>
  <div class="panel-body">
    <form class="form-inline" id="form" v-on:submit.prevent="addSong">
<div class="form-group">
  <label for="songName">Name:</label>
  <input type="text" id="songName" class="form-control" v-model="newSong.name">
</div>
<div class="form-group">
  <label for="songLink">Link:</label>
  <input type="text" id="songLink" class="form-control" v-model="newSong.link">
</div>
<input class="btn btn-primary" value="Add Song" type="submit">
</input>
    </form>
  </div>
  <div>

    <div class="panel panel-default">
        <div class="panel-heading">
          <h3>Music List</h3>
        </div>
        <div class="panel-body">
          <table class="table table-striped">
            <thead>
              <tr>
                <th>Name</th>
                <th>Link</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="song in album">
                <td>
                  {{song.name}}
                </td>
                <td>
                  <a v-bind:href="song.link" target="_blank">
                  {{song.link}}</a>
                </td>
                <tr>
            </tbody>
          </table>
        </div>
      </div>
</template>

<script>
import Hello from './components/Hello'
import Firebase from 'firebase'

let config = {

}

let app = Firebase.initializeApp(config)
let db = app.database()

let musicRef = db.ref('album')

export default {
  name: 'app',
  firebase: {
    album: musicRef
  },
  data () {
    return {
      newSong: {
        name:'',
        link:''
      }
    }
  },
  methods: {
    addSong: function(){
      musicRef.push(this.newSong)
      this.newSong.name = ''
      this.newSong.link = ''
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
