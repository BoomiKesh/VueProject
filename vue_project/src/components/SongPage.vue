<template>
  <div class="song-page">
    <div class="song-container">
      <div class="song-info">
        <img
            :src="song.img"
            :alt="song.title"
            class="song-info__image"
        />
        <div class="song-info__content">
          <div class="song-info__title">{{ song.title }}</div>
          <div class="song-info__author">{{ song.author }}</div>
          <div class="song-info__year">{{ song.year }}</div>
        </div>
      </div>

      <div class="song-lyrics">
        <div class="lyrics-title">Текст песни</div>
        <div class="lyrics-content">{{ song.lyrics }}</div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  props:{
    song:{
      type:Object,
      required:true
    }
  }
}
</script>

<style scoped>
.song-page {
  min-height: 60px;
  background-color: #1a1a1a;
  padding: 30px;
  width: 1000px;
  box-sizing: border-box;
}

.song-container {
  max-width: 1400px;
  margin: 0 auto;
  display: flex;
  gap: 40px;
  align-items: flex-start;
}

.song-info {
  background-color: #2d2d2d;
  border-radius: 8px;
  padding: 25px;
  flex: 0 0 350px;
  position: sticky;
  top: 90px;
}

.song-info__image {
  width: 100%;
  aspect-ratio: 1/1;
  object-fit: cover;
  border-radius: 6px;
  margin-bottom: 20px;
}

.song-info__title {
  color: #fff;
  font-size: 24px;
  font-weight: 600;
  margin-bottom: 8px;
  line-height: 1.3;
}

.song-info__author {
  color: #aaa;
  font-size: 18px;
  margin-bottom: 5px;
}

.song-info__year {
  color: #777;
  font-size: 16px;
}

.song-lyrics {
  background-color: #2d2d2d;
  border-radius: 8px;
  padding: 30px;
  flex: 1;
  min-width: 0;
}

.lyrics-title {
  color: #fff;
  font-size: 22px;
  font-weight: 600;
  margin-bottom: 25px;
  padding-bottom: 15px;
  border-bottom: 1px solid #3a3a3a;
}

.lyrics-content {
  color: #e0e0e0;
  font-size: 18px;
  line-height: 1.7;
  white-space: pre-line;
  word-wrap: break-word;
  overflow-wrap: break-word;
}

</style>