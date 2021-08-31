<template>
  <div id="app">
    <div id="nav">
      <header><h1>My Music</h1></header>

      <section class="player">
        <h2 class="song-title">
          {{ current.title }} - <span> {{ current.artist }}</span>
        </h2>
        <div class="controls">
          <button class="control-btn prev" @click="prev">
            <i class="fas fa-caret-left"></i>
          </button>
          <button
            class="control-btn play"
            v-if="isPlaying == false"
            @click="play"
          >
            <i class="fas fa-play"></i>
          </button>
          <button class="control-btn pause" v-else @click="pause">
            <i class="fas fa-pause"></i>
          </button>
          <button class="control-btn next" @click="next">
            <i class="fas fa-caret-right"></i>
          </button>
        </div>
      </section>
      <section class="playlist"></section>
      <h2>PlayList</h2>
      <button
        v-for="song in songs"
        :key="song.src"
        @click="play(song)"
        :class="song.src == current.src ? 'song playing' : 'song'"
      >
        {{ song.title }} - {{ song.artist }}
      </button>
    </div>
  </div>
</template>
<script>
export default {
  name: "MusicApp",
  data() {
    return {
      current: {},
      index: 0,
      isPlaying: false,
      songs: [
        {
          title: "Barai-Ba-K",
          artist: "Kashif Din",
          src: require("../assets/Barai-Ba-K.mp3"),
        },
        {
          title: "Bewajah_OST",
          artist: "Nabeel Shoukat Ali",
          src: require("../assets/Bewajah_OST.mp3"),
        },
        {
          title: "Charat e Baait",
          artist: "Kashif Din",
          src: require("../assets/Charati_e_Baait.mp3"),
        },
        // {
        //   title: "Despacito Instrumental",
        //   artist: "Baceeto",
        //   src: require("../assets/Despacito_Rubab.au"),
        // },
      ],
      player: new Audio(),
    };
  },
  methods: {
    play(song) {
      if (typeof song.src !== "undefined") {
        this.current = song;
        this.player.src = this.current.src;
      }
      this.player.play();
      // this.player.addEventListener("ended", function () {
      //   this.index++;
      //   if (this.index > this.songs.length - 1) {
      //     this.index = 0;
      //   }
      //   this.current = this.songs[this.index];
      //   this.play(this.current);
      // });
      this.isPlaying = true;
    },
    pause() {
      this.player.pause();
      this.isPlaying = false;
    },
    next() {
      this.index++;
      if (this.index > this.songs.length - 1) {
        this.index = 0;
      }
      this.current = this.songs[this.index];
      this.play(this.current);
    },
    prev() {
      this.index--;
      if (this.index < 0) {
        this.index = this.songs.length - 1;
      }
      this.current = this.songs[this.index];
      this.play(this.current);
    },
  },
  // created() {
  //   this.current = this.songs[this.index];
  //   this.player.src = this.current.src;
  //   this.player.play();
  // },
};
</script>
<style>
body {
  padding: 0;
  margin: 0;
}
#app {
  width: 26%;
  margin: auto;
  margin-top: 100px;
}
@media screen and (max-width: 900px) {
  #app {
    width: 50%;
  }
}
@media screen and (max-width: 719px) {
  #app {
    width: 80%;
  }
}
@media screen and (max-width: 560px) {
  #app {
    width: 90%;
  }
}
#nav {
  border: 1px solid;
  box-shadow: 5px 10px brown;
  padding: 20px;

}
header {
  margin-top: -22px;
  background-color: brown;
  text-align: center;
  padding: 10px;
}
header h1 {
  margin-top: 36px;
  color: white;
}
.player {
  margin: 20px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
.song-title {
  text-align: center;
}
.control-btn {
  margin: auto 20px;
}
.song {
  margin: 10px auto;
  min-width: 240px;
  width: 80%;
  border: none;
  outline: none;
  background-color: brown;
  display: block;
  padding: 14px;
  border-radius: 10px;
}
.song:hover {
  color: rgb(255, 255, 255);
}
.playing {
  color: white;
}
</style>
