<script setup lang="ts">
import { ref, computed } from "vue";
import { songs, type Song } from "./data/songs";

const query = ref("");
const selected = ref<Song | null>(null);

const filtered = computed(() =>
  songs.filter(s =>
    s.title.toLowerCase().includes(query.value.toLowerCase())
  )
);
</script>

<template>
  <div class="app">
    <h1>🌈 Super Music World 🎵</h1>

    <input
      v-model="query"
      placeholder="Search a song 🎤"
      class="search"
    />

    <div class="song-list">
      <button
        v-for="song in filtered"
        :key="song.title"
        class="song-button"
        @click="selected = song"
      >
        🎶 {{ song.title }}
      </button>
    </div>

    <div v-if="selected" class="player">
      <h2>✨ {{ selected.title }}</h2>

      <iframe
        class="video"
        :src="`https://www.youtube.com/embed/${selected.youtubeId}`"
        allowfullscreen
      ></iframe>

      <div class="lyrics">
        <h3>🎤 Sing Along</h3>
        <p>{{ selected.lyrics }}</p>
      </div>
    </div>
  </div>
</template>

<style>
body {
  margin: 0;
  font-family: "Comic Sans MS", cursive;
  background: linear-gradient(135deg, #ffecd2, #fcb69f);
}

.app {
  text-align: center;
  padding: 20px;
}

h1 {
  color: #ff4081;
}

.search {
  padding: 12px;
  border-radius: 25px;
  border: none;
  width: 250px;
  margin: 15px;
}

.song-list {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}

.song-button {
  margin: 8px;
  padding: 12px 20px;
  border-radius: 25px;
  border: none;
  background: #4fc3f7;
  color: white;
  cursor: pointer;
  transition: transform 0.2s;
}

.song-button:hover {
  transform: scale(1.1);
}

.video {
  width: 320px;
  height: 200px;
  border-radius: 20px;
  margin-top: 10px;
}

.lyrics {
  margin-top: 15px;
  padding: 15px;
  background: #fff9c4;
  border-radius: 20px;
}
</style>