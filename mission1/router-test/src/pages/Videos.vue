<template>
  <div class="card card-body">
    <h2 class="m-3">영상 리스트</h2>
    <ul class="list-group">
      <li
        v-for="v in videos"
        :key="v.id"
        class="list-group-item text-left"
        :class="playingVideo(v.id)"
      >
        {{ v.title }} ( {{ v.category }})
        <router-link :to="{ name: 'videos/id', params: { id: v.id } }">
          <span class="float-end badge bg-secondary">듣기</span>
        </router-link>
      </li>
    </ul>
  </div>
</template>

<script>
import YoutubeVue3 from 'youtube-vue3';
import { inject } from 'vue';
import { useRoute } from 'vue-router';

export default {
  // name: 'VideoPlayer',
  name: 'Videos',
  components: { YoutubeVue3 },
  setup() {
    // videos 정의가 없어서 교안에 없는 부분추가
    const videos = inject('videos');
    const route = useRoute();

    const stopVideo = () => {
      playerRef.value.player.stopVideo();
      router.push({ name: 'videos' });
    };
    const playNext = () => {
      const index = videos.findIndex((v) => v.id === videoInfo.video.id);
      const nextVideo = videos[index + 1];
      if (nextVideo) {
        videoInfo.video = nextVideo;
        router.push({ name: 'videos/id', params: { id: nextVideo.id } });
      } else {
        videoInfo.video = video[0];
        router.push({ name: 'videos/id', params: { id: videos[0].id } });
      }
    };
    return {
      // //videoInfo,
      // playerRef,
      // stopVideo,
      // playPrev,
      videos,
    };
  },
};
</script>
