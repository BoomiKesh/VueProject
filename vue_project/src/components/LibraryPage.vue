<template>
  <div class="library-page">
    <h1 class="library-title">Медиатека</h1>

    <div class="songs-grid">
      <SongCard
          v-for="(item, index) in addedSongs"
          @render-song = "renderSong"
          @add-song="addToLibrary"
          @delete-song="deleteFromLibrary"
          :key="item.id"
          :song="item"
          :index="index"
          class="song-card-item"
      />
    </div>

    <div v-if="addedSongs.length === 0" class="empty-library">
      В библиотеке пока нет песен
    </div>
  </div>
</template>
<script>
import SongCard from "@/components/SongCard.vue";

export default {
  components: {SongCard},
  props:{
    songs:{
      type: Array,
      required:true,
    }
  },

  computed: {
    addedSongs() {
      return this.songs.filter(song => song.isAdded === true);
    }
  },

  methods:{
    renderSong(id){
      this.$emit('render-song', id);
    },

    addToLibrary(id){
      for(let i = 0; i < this.songs.length; i++){
        if (this.songs.at(i).id === id){
          this.songs.at(i).isAdded = true;
        }
      }
      this.$emit('add-song', id);
    },

    deleteFromLibrary(id){
      console.log("LibraryPage");
      for(let i = 0; i < this.songs.length; i++){
        if (this.songs.at(i).id === id){
          console.log(this.songs.at(i).isAdded);
          this.songs.at(i).isAdded = false;
          console.log(this.songs.at(i).isAdded);
        }
      }
      this.$emit('delete-song', id);
    }
  }

}
</script>

<style scoped>
.library-page {
  min-height: 100vh;
  background-color: #1a1a1a;
  padding: 20px;
  color: #ffffff;
}

.library-title {
  font-size: 28px;
  margin-bottom: 30px;
  text-align: center;
}

.songs-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
  gap: 25px;
  max-width: 1200px;
  margin: 0 auto;
}

.empty-library {
  text-align: center;
  font-size: 18px;
  color: #999;
  padding: 50px 0;
}
</style>
