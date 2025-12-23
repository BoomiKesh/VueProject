<template>
  <div class="app-container">
    <header class="app-header">
      <div class="header-content">
        <h1 class="logo">Музыка</h1>
        <nav class="nav-buttons">
          <button
              class="nav-btn"
              :class="{ active: currentPage === 'Search' }"
              @click="currentPage = 'Search'"
          >
            Поиск
          </button>
          <button
              class="nav-btn"
              :class="{ active: currentPage === 'Library' }"
              @click="currentPage = 'Library'"
          >
            Моя медиатека
          </button>
        </nav>
      </div>
    </header>
    <main class="main-content">
      <component
          :is="currentPageComponent"
          :songs="currentSongs"
          :song="selectedSong"
          @render-song="renderSong"
          @delete-song="deleteSong"
          @add-song="addSong"
      />
    </main>
  </div>
</template>
<script>
  import SearchPage from "@/components/SearchPage.vue";
  import LibraryPage from "@/components/LibraryPage.vue";
  import songs from "@/resources/songs.js";
  import SongPage from "@/components/SongPage.vue";

  export default {
    name:'App',
    components: {SongPage},
    data() {
      return {
        currentPage: 'Library',
        currentSongs: songs,
        songId: null,
      }
    },

    computed:{
      currentPageComponent() {
        switch (this.currentPage){
          case 'Search':
            return SearchPage
          case 'Library':
            return LibraryPage
          case 'Song':
            return SongPage
          default:
            return LibraryPage
        }
      },

      selectedSong() {
        for(const song of songs){
          if (song.id === this.songId){
            return song;
          }
        }
        return false;
      }
    },

    methods:{
      renderSong(id){
        this.songId = id;
        this.currentPage = 'Song';
      },

      addSong(id){
        for(let i = 0; i < this.currentSongs.length; i++){
          if (this.currentSongs.at(i).id === id){
            this.currentSongs.at(i).isAdded = true;
          }
        }
      },

      deleteSong(id){
        for(let i = 0; i < this.currentSongs.length; i++){
          if (this.currentSongs.at(i).id === id){
            this.currentSongs.at(i).isAdded = false;
          }
        }
      }
    }
  }
</script>


<style scoped>

.app-container {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  background-color: #1a1a1a;
}

.app-header {
  background-color: #2d2d2d;
  border-bottom: 1px solid #3a3a3a;
  padding: 0 20px;
  position: sticky;
  top: 0;
  z-index: 100;
  width: 100%;
  box-sizing: border-box;
}

.header-content {
  margin: 0 auto;
  display: flex;
  align-items: center;
  justify-content: space-between;
  height: 60px;
}

.logo {
  color: #fff;
  font-size: 24px;
  font-weight: 600;
  margin: 0;
}

.nav-buttons {
  display: flex;
  gap: 15px;
}

.nav-btn {
  background: none;
  border: none;
  color: #aaa;
  font-size: 16px;
  padding: 8px 16px;
  border-radius: 4px;
  cursor: pointer;
  transition: all 0.2s ease;
}

.nav-btn:hover {
  background-color: #3a3a3a;
  color: #fff;
}

.nav-btn.active {
  background-color: #404040;
  color: #fff;
  font-weight: 500;
}

.main-content {
  flex: 1;
}

</style>
