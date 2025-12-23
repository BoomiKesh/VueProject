<template>
  <div class="song-card">
    <img
        :src="song.img"
        :alt="song.title"
        class="song-image"
        @click="renderSong()"
    />
    <div class="song-title">{{ song.title }}</div>
    <div class="song-author">{{ song.author }}</div>
    <div class="song-year">{{ song.year }}</div>
    <button v-if="!song.isAdded" @click="addToLibrary()" class="song-button__add">Добавить в медиатеку</button>
    <button  v-if="song.isAdded" @click="deleteFromLibrary()" class="song-button__delete">Убрать из медиатеки</button>
  </div>
</template>
<script>
export default {
  props:{
    song:{
      type:Object,
      required:true
    }
  },

  methods:{
    renderSong(){
      this.$emit('render-song', this.song.id);
    },

    addToLibrary(){
      this.$emit('add-song', this.song.id);
    },

    deleteFromLibrary(){
      console.log("SongCard");
      this.$emit('delete-song', this.song.id);
    }


  }
}
</script>

<style scoped>
.song-card {
  background-color: #2d2d2d;
  border-radius: 6px;
  padding: 15px;
  cursor: pointer;
  display: flex;
  flex-direction: column;
  gap: 8px;
}


.song-image {
  width: 100%;
  aspect-ratio: 1/1;
  object-fit: cover;
  border-radius: 4px;
  margin-bottom: 10px;
}

.song-title {
  font-weight: 600;
  font-size: 16px;
  color: #fff;
  white-space: nowrap;
  overflow: hidden;
}

.song-author {
  font-size: 14px;
  color: #aaa;
}

.song-year {
  font-size: 12px;
  color: #777;
}
</style>