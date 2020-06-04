<template>
  <div id="app">
    <header>
      <h1>My Music</h1>    
    </header>
    <main>
      <section class="player">
        <h2 class="song-title">{{ current.title }} - <span>{{ current.artist }}</span>  </h2>
        <div class="controls">
          <button class="prev" @click="prev">Prev</button>
          <button class="play" v-if="!isPlaying" @click="play">Play</button>
          <button class="pause" v-else @click="pause">Pause</button>
          <button class="next" @click="next">Next</button>
        </div>
      </section>
      <section class="playlist">
          <h3>The Playlist</h3>
          <button v-for="song in songs" :key="song.src" @click="play(song)" :class="(song.src == current.src) ? 'song playing' : 'song stop'">
            {{ song.title }} - {{ song.artist }}
          </button>
      </section>
    </main>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      current: {
        title: 'No Title',
        artist: 'No Artist'
      },
      index : 0,
      isPlaying: false,
      songs : [
        {
          title: 'Melankolia',
          artist: 'Efek Rumah Kaca',
          src: require('./assets/src/melankolia.mp3')
        },
        {
          title: 'Kamar Gelap',
          artist: 'Efek Rumah Kaca',
          src: require('./assets/src/kamar_gelap.mp3')
        },
        {
          title: 'Kuning',
          artist: 'Efek Rumah Kaca',
          src: require('D:\\Downloads\\IDM\\Music\\kuning.mp3')
        },
      ],
      player : new Audio()
    }
  },
  methods: {
    play(song){
      if(song.src != undefined){
        this.current = song;
        this.player.src = this.current.src;
      }

      this.player.play();
      this.isPlaying = true;
    },
    pause(){
      this.player.pause();
      this.isPlaying = false;
    },
    prev(){
      this.index--;

      if(this.index < 0) {
        this.index = this.songs.length-1;
      }

      this.current = this.songs[this.index];
      this.play(this.current);
    },
    next(){
      this.index++;

      if(this.index > this.songs.length-1) {
        this.index = 0;
      }

      this.current = this.songs[this.index];
      this.play(this.current);
    }
  },
  created() {
    this.current = this.songs[this.index];
    this.player.src = this.current.src;
    this.player.play();
  },
}
</script>

<style>
*{
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}

body, html{
  font-family: sans-serif;
  height: 100%;
}

#app{
  background-image: url('./assets/bg1.jpg');
  background-size: cover;
  background-position: bottom;
  transition: 0.4s;
  height: 100%;
}

header{
  display: flex;
  justify-content: center;
  align-items: center;
  background: #212121;
  padding: 10px;
  color: #fff;
}

main{
  width: 100%;
  max-width: 768px;
  margin: 50px auto;
  padding: 25px;
  border-radius: 10px;
  background-image: linear-gradient(to top, rgba(0, 0, 0, 0.25), rgba(0, 0, 0, 0.75));
}

.song-title{
  color: #fff;
  font-size: 32px;
  font-weight: 700;
  text-transform: uppercase;
  text-align: center;
  text-shadow: 1px 3px rgba(0, 0, 0, 0.25);
}

.song-title span{
  font-style: italic;
  font-weight: 400;
}

.controls{
  display: flex;
  justify-content: center;
  padding: 30px 15px;
}

button{
  appearance: none;
  background: none;
  border: none;
  outline: none;
  cursor: pointer;
  box-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}

.play, .pause{
  font-size: 20px;
  font-weight: 700;
  background-color: #cc2e5d;
  padding: 15px 25px;
  margin: 0px 15px;
  border-radius: 8px;
  color: #fff;
}

.prev, .next{
  font-size: 14px;
  font-weight: 700;
  padding: 5px 20px;
  margin: 0px 15px;
  border-radius: 6px;
  color: #fff;
  background-color: #ff5858;
}

.playlist{
  margin: 0px 30px;
}

.playlist h3{
  font-size: 28px;
  font-weight: 500;
  text-align: center;
  color: #fff; 
  margin-bottom: 30px;
  text-shadow: 1px 3px rgba(0, 0, 0, 0.25);
}

.playlist button{
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 10px 20px;
}

.playlist .song{
  display: block;
  width: 100%;
  padding: 15px;
  font-size: 20px;
  font-weight: 700;
  cursor: pointer;
}

.playlist .song:hover{
  color: #fff;
  background-image: linear-gradient(to left, #cc2e5d, #ff5858);
}

.playlist .playing{
  color: #fff;
  background-image: linear-gradient(to right, #cc2e5d, #ff5858);
  transition: 0.3s;
}

.playlist .stop{
  display: none;
}

</style>
