<script setup lang="ts">
import { ref, reactive } from 'vue';

// 轮播图数据
const albums = [
  {
    id: 1,
    title: 'HIT ME HARD AND SOFT',
    info: '"碧梨"Billie Eilish第三张录音室专辑《HIT ME HARD AND SOFT》正式全球发行，主打曲目为《LUNCH》！作为Billie Eilish的第三张录音室专辑，这张备受"碧梨"所珍爱的全新专辑依旧由Billie Eilish与FINNEAS联袂创作呈现，FINNEAS担纲专辑制作，共收录10首曲目。从首张专辑《WHEN WE ALL FALL ASLEEP, WHERE DO WE GO?》光怪陆离的暗黑宇宙到《Happier Than Ever》中高亢而激烈的人声演绎，Billie Eilish将《HIT ME HARD AND SOFT》视为重返自我的本真之旅。"我享受当事物变得激烈之时的刺激爽快感，也喜欢被温柔以待时的甜蜜。我想要在其间寻觅两者兼得的模式，尽管这在现实生活中往往难以被达成"，Billie Eilish如此介绍新专辑《HIT ME HARD AND SOFT》。《HIT ME HARD AND SOFT》涵盖一系列多样化的听感歌曲，同时在曲序编排上保持极强的统一性，是一张值得从头到尾完整聆听的专辑力作。',
    cover: '/1.webp'
  },
  {
    id: 2,
    title: 'Happier Than Ever',
    info: 'Billie Eilish全新佳作的个人第二张录音室专辑--《Happier Than Ever》，于2021年7月30日正式完整释出。继荣获多项格莱美奖项肯定、打破无数纪录的首张个人专辑《WHEN WE ALL FALL ASLEEP, WHERE DO WE GO?》后，《Happier Than Ever》依旧凭借兄妹二人实力"独挑大梁"完成，由19岁的Billie Eilish担纲创作，哥哥FINNEAS挎刀制作。自出道单曲《ocean eyes》发布以来，Billie Eilish迅速成为令全球乐坛瞩目的未来之星，不断以极具个人特色的独特音乐风格打破流行乐的种种束缚与限制。自2015年脱颖而出后不久，Billie的首张个人录音室专辑《WHEN WE ALL FALL ASLEEP, WHERE DO WE GO?》在2019年势如破竹般地空降美国公告牌专辑榜与其他17个地区的专辑榜冠军，同时也成为了此年度收获最多流媒体播放量的专辑。《WHEN WE ALL FALL ASLEEP, WHERE DO WE GO?》完全由Billie与她的哥哥FINNEAS二人在洛杉矶的家中完成专辑中的歌曲谱写、录音以及制作过程。此后， Billie Eilish持续创造并刷新着乐坛历史纪录.',
    cover: '/2.webp'
  },
  {
    id: 3,
    title: 'WHEN WE AL FALL ASLEEP, WHERE DO WE GO?',
    info: '年仅17岁即成为全球最耀眼的流量偶像，唱作新天后Billie Eilish终于发布了她的个人首张录音室专辑《WHEN WE ALL FALL ASLEEP, WHERE DO WE GO?》。Billie Eilish迅速成为全球巨星可谓是现象级的，这样的成就迄今止也是无与伦比的。自从首发单曲"Ocean Eyes"问世以来，Billie已悄然步入了流行乐坛的前沿。归功于全球越来越多的忠实乐迷，她2017年发行的首张EP《Don\'t Smile at Me》至今一年半的时间过去了，却仍然在Billboard Hot 200专辑榜占据一席之地，并且在全球狂揽50亿试听总量。她的巡演更是在全球热卖到屡屡售罄。她被殿堂级的摇滚乐队Nirvana鼓手Dave Grohl盛赞"宛如新时代的Nirvana",在Billie的首张专辑中,充满了奇思妙想.',
    cover: '/3.webp'
  }
];

// 当前轮播图索引
const currentIndex = ref(0);

// 自动轮播
let carouselInterval = setInterval(() => {
  currentIndex.value = (currentIndex.value + 1) % albums.length;
}, 3000);

// 手动切换轮播图
const goToSlide = (index: number) => {
  currentIndex.value = index;
  // 重置自动轮播
  clearInterval(carouselInterval);
  carouselInterval = setInterval(() => {
    currentIndex.value = (currentIndex.value + 1) % albums.length;
  }, 3000);
};

// 音乐播放控制
const audioRef = ref<HTMLAudioElement | null>(null);
const isPlaying = ref(false);
const volume = ref(0.5);

const togglePlayPause = () => {
  if (audioRef.value) {
    if (isPlaying.value) {
      audioRef.value.pause();
    } else {
      audioRef.value.play();
    }
    isPlaying.value = !isPlaying.value;
  }
};

const handleVolumeChange = () => {
  if (audioRef.value) {
    audioRef.value.volume = volume.value;
  }
};

// 歌手信息
const singerInfo = {
  name: 'Billie Eilish',
  bio: 'Billie Eilish Pirate Baird O\'Connell 是一位美国创作歌手，以其独特的音乐风格和视觉形象而闻名。她于2015年凭借歌曲《Ocean Eyes》首次亮相，并迅速成为全球知名的艺术家。她的音乐融合了流行、电子和另类R&B元素，歌词常常探讨心理健康、成长和社会问题等主题。至今，比莉·艾利什共获得2项奥斯卡金像奖、10项格莱美奖，成为最年轻包揽格莱美奖四个通类奖项的艺人。她还曾入选《时代周刊》"全球最具影响力百人榜"，并被BBC评为"全球100位最具影响力女性"。作为第一位两次获得Apple music年度艺人的歌手，比莉·艾利什的音乐才华和影响力不容小觑。2024年5月发行的新专辑《HIT ME HARD AND SOFT》在全球 138个国家和地区的全类型专辑排行第1。2026年，其演唱的歌曲《WILDFLOWER》获得第68届格莱美奖年度歌曲。再次证明她的音乐实力。',
  image: '/BillieEilish.webp'
};

const songInfo = {
  name: 'BIRDS OF A FEATHER',
  image: '/BIRDS_OF_A_FEATHER.webp',
  audio: '/BIRDS_OF_A_FEATHER.mp3'
}
</script>

<template>
  <div class="container">
    <!-- 顶部轮播图 -->
    <div class="carousel">
      <div class="carousel-container">
        <div
          v-for="(album, index) in albums"
          :key="album.id"
          class="carousel-slide"
          :class="{ 'active': index === currentIndex }"
        >
          <div class="album-image">
            <img :src="album.cover" :alt="album.title" />
          </div>

          <div class="album-info">
            <h3>{{ album.title }}</h3>
            <p>{{ album.info }}</p>
          </div>
        </div>
      </div>

      <!-- 轮播指示器 -->
      <div class="carousel-indicators">
        <span
          v-for="(album, index) in albums"
          :key="album.id"
          :class="{ 'active': index === currentIndex }"
          @click="goToSlide(index)"
        ></span>
      </div>
    </div>

    <!-- 中间内容区域 -->
    <div class="content">
      <div class="image-section">
        <img :src="singerInfo.image" :alt="singerInfo.name" class="singer-image" />
      </div>

      <div class="info-section">
        <h1>{{ singerInfo.name }}</h1>
        <p class="bio">{{ singerInfo.bio }}</p>
      </div>
    </div>

    <!-- 底部音乐播放器 -->
    <div class="music-player">
      <div class="player-image">
        <img :src="songInfo.image" :alt="songInfo.name" class="song-image" />
      </div>
      <div class="player-info">
        <h3>{{ songInfo.name }}</h3>
        <div class="player-controls">
          <button @click="togglePlayPause" class="play-btn">
            {{ isPlaying ? '暂停' : '播放' }}
          </button>

          <div class="volume-control">
            <label for="volume-slider">音量:</label>
            <input
              type="range"
              id="volume-slider"
              min="0"
              max="1"
              step="0.01"
              v-model="volume"
              @input="handleVolumeChange"
            />
          </div>
        </div>
      </div>

      <audio ref="audioRef" :volume="volume">
        <source :src="songInfo.audio" type="audio/mpeg" />
        您的浏览器不支持音频元素。
      </audio>
    </div>
  </div>
</template>

<style>
body, html {
  height: 100%;
  margin: 0;
  padding: 0;
  background-color: #2f2f2f;
}


</style>

<style scoped>
/* 容器样式 */
.container {
  background-color: #2f2f2f;
  min-height: 100vh;
  padding: 0;
  width: 90%;
  margin: 0 auto;
  font-family: Arial, sans-serif;
  color: #ffffff;
}
/* 轮播图样式 */
.carousel {
  background-color: #72dd72;
  margin-top: 50px;
  margin-bottom: 30px;
  text-align: center;
  flex-wrap: wrap;
}
/* 轮播图容器样式 */
.carousel-container {
  background-color: #fff;
  border-radius: 10px;
  margin: 0 auto;
  width: 92%;
  position: relative;
  overflow: hidden;
  height: auto;
  min-height: 300px;
  border-radius: 5px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}
/* 轮播图滑块样式 */
.carousel-slide {
  display: flex;
  justify-content: center;
  align-items: flex-start;
  gap: 30px;
  margin-top: 30px;
  margin-bottom: 30px;
  position: absolute;
  opacity: 0;
  transition: opacity 0.5s ease-in-out;
}
/* 轮播图滑块激活样式 */
.carousel-slide.active {
  opacity: 1;
}
/* 轮播图滑块图片样式 */
.carousel-slide img {
  max-width: 80%;
  max-height: 70%;
  object-fit: contain;
  border-radius: 5px;
}
/* 轮播图指示器样式 */
.carousel-indicators {
  display: flex;
  justify-content: center;
  margin-top: 15px;
}
/* 轮播图指示器样式样式 */
.carousel-indicators span {
  width: 12px;
  height: 12px;
  border-radius: 50%;
  background-color: #bbb;
  margin: 0 10px;
  margin-bottom: 10px;
  cursor: pointer;
  transition: background-color 0.3s;
}
/* 轮播图指示器激活样式 */
.carousel-indicators span.active {
  background-color: #49c134;
}
/* 轮播图滑块信息样式 */
.album-image {
  flex: 1;
  min-width: 300px;
  text-align: center;
}

.album-info {
  flex: 4;
  min-width: 300px;
  margin-top: 0px;
  text-align: left;
  justify-self: flex-start;
  flex-wrap: wrap;
}
/* 轮播图滑块信息标题样式 */
.album-info h3 {
  margin-top: 0px;
  font-size: 1.2em;
  color: #333;
}
/* 轮播图滑块信息内容样式 */
.album-info p {
  margin-top: 10px;
  font-size: 0.5em;
  color: #333;
}
/* 中间内容区域样式 */
.content {
  display: flex;
  justify-content: center;
  align-items: flex-start;
  gap: 30px;
  margin-bottom: 30px;
  flex-wrap: wrap;
}
/* 中间内容区域图片样式 */
.image-section {
  flex: 1;
  min-width: 300px;
  text-align: center;
}
/* 中间内容区域图片样式 */
.singer-image {
  width: 100%;
  max-width: 400px;
  height: auto;
  border-radius: 10px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}
/* 中间内容区域信息样式 */
.info-section {
  flex: 2;
  min-width: 300px;
  padding: 20px;
}
/* 中间内容区域信息标题样式 */
.info-section h1 {
  font-size: 2em;
  margin-bottom: 15px;
  color: #ffffff;
}
/* 中间内容区域信息内容样式 */
.bio {
  font-size: 1em;
  line-height: 1.6;
  text-align: justify;
}
/* 底部音乐播放器样式 */
.music-player {
  display: flex;
  text-align: center;
  padding: 20px;
  background-color: #72dd72;
  border-radius: 10px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  margin-top: 20px;
}
/* 底部音乐播放器标题样式 */
.music-player h3 {
  margin-bottom: 15px;
  font-size: 1.5em;
}
/* 底部音乐播放器图片样式 */
.song-image {
  width: 70%;
  max-width: 500px;
  height: auto;
  border-radius: 10px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}
/* 底部音乐播放器图片样式 */
.player-image{
  flex: 1;
  margin-right: 0px;
  justify-content:center;
  align-items: center;
}
/* 底部音乐播放器信息样式 */
.player-info {
  flex: 2;
  text-align: left;
  justify-content: center;
  align-items: flex-start;
  min-width: 300px;
  padding: 20px;
}
/* 底部音乐播放器控制样式样式 */
.player-controls {
  display: flex;
  gap: 20px;
  margin-bottom: 15px;
  flex-wrap: wrap;
}
/* 底部音乐播放器控制样式样式 */
.play-btn {
  padding: 10px 20px;
  font-size: 1em;
  background-color: #333;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s;
}
/* 底部音乐播放器控制样式样式 */
.play-btn:hover {
  background-color: #555;
}
/* 底部音乐播放器控制样式样式 */
.volume-control {
  display: flex;
  align-items: center;
  gap: 10px;
}
/* 底部音乐播放器控制样式样式 */
.volume-control label {
  font-size: 1em;
}
/* 底部音乐播放器控制样式样式 */
#volume-slider {
  width: 150px;
}

/* 响应式设计 */
@media (max-width: 768px) {
  .content {
    flex-direction: column;
    align-items: center;
  }

  .image-section,
  .info-section {
    min-width: auto;
    width: 100%;
    text-align: center;
  }

  .carousel-slide {
    flex-direction: column;
    align-items: center;
  }

  .album-image,
  .album-info {
    min-width: auto;
    width: 100%;
    text-align: center;
  }

  .player-controls {
    flex-direction: column;
  }
}
</style>
