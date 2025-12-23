<template>
  <div class="search-page">
    <h1 class="search-title">Поиск песен</h1>

    <input
        class="search-bar"
        type="text"
        v-model="searchText"
        placeholder="Введите название либо слова песни"
    >

    <div class="songs-grid">
      <SongCard
          v-for="(item, index) in filteredSongs"
          @render-song="renderSong"
          @add-song="addToLibrary"
          @delete-song="deleteFromLibrary"
          :key="item.id"
          :song="item"
          :index="index"
          class="main-card"
      />
    </div>

    <div v-if="songs.length === 0 && searchText" class="no-results">
      По запросу "{{ searchText }}" ничего не найдено
    </div>
  </div>
</template>
<script>
import SongCard from "@/components/SongCard.vue";

export default {
  components: {SongCard},
  data(){
    return{
      searchText: '',
    };
  },

  props:{
    songs:{
      type: Array,
      required: true,
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
      for(let i = 0; i < this.songs.length; i++){
        if (this.songs.at(i).id === id){
          this.songs.at(i).isAdded = false;
        }
      }
      this.$emit('delete-song', id);
    }
  },

  computed: {
    filteredSongs() {
      if (!this.searchText.trim()) {
        return this.songs;
      }

      const searchText = this.searchText.toLowerCase();

      return this.songs.filter(song => {
        const title = song.title.toLowerCase();
        const lyrics = song.lyrics.toLowerCase();

        return title.includes(searchText) || lyrics.includes(searchText);
      });
    }
  },
}
</script>

<style scoped>
.search-page {
  min-height: 100vh;
  background-color: #1a1a1a;
  padding: 20px;
  color: #ffffff;
}

.search-title {
  font-size: 28px;
  margin-bottom: 30px;
  text-align: center;
}

.search-bar {
  width: 100%;
  max-width: 600px;
  display: block;
  margin: 0 auto 40px auto;
  padding: 14px 20px;
  font-size: 16px;
  background-color: #2d2d2d;
  border: 1px solid #3a3a3a;
  border-radius: 8px;
  color: #fff;
}

.search-bar::placeholder {
  color: #888;
}

.songs-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
  gap: 25px;
  max-width: 1200px;
  margin: 0 auto;
}

.no-results {
  text-align: center;
  font-size: 18px;
  color: #999;
  padding: 50px 0;
}
</style>