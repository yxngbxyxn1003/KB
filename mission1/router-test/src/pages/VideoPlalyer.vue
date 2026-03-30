<template>
  <div>
    <h2>VideoPlayer</h2>
  </div>
</template>

<script>
import { reactive, ref, inject } from 'vue';
import { useRoute, useRouter, onBeforeRouteUpdate } from 'vue-router';
import { YoutubeVue3 } from 'youtube-vue3';

export default {
  name: 'VideoPlayer',
  components: { YoutubeVue3 },
  setup() {
    const videos = inject('videos');
    const playerRef = ref(null);
    const currentRoute = useRoute();
    const router = useRouter();
    let videoInfo, currentIndex, prevVideoId, nextVideoId;
    videoInfo = reactive({
      video: videos.find((v) => v.id === currentRoute.params.id),
    });

    const getNavId = (to) => {
      videoInfo.video = videos.find((v) => v.id === to.params.id);
      currentIndex = videos.findIndex((v) => v.id === videoInfo.video.id);
      prevVideoId = videos[currentIndex - 1]
        ? videos[currentIndex - 1].id
        : null;
      nextVideoId = videos[currentIndex + 1]
        ? videos[currentIndex + 1].id
        : null;
    };

    // 마운트되었을 때 현재의 라우트 정보를 이용해 이전 , 다음 ID 획득
    getNavId(currentRoute);
    const stopVideo = () => {
      playerRef.value.player.stopVideo();
      router.push({ name: 'videos' });
    };
    const playNext = () => {
      if (nextVideoId)
        router.push({ name: 'videos/id', params: { id: nextVideoId } });
      else router.push({ name: 'videos/id', params: { id: videos[0].id } });
    };
    const playPrev = () => {
      if (prevVideoId)
        router.push({ name: 'videos/id', params: { id: prevVideoId } });
    };
    onBeforeRouteUpdate((to) => {
      getNavId(to);
    });
    return { videoInfo, playerRef, playNext, stopVideo, playPrev };
  },
};
</script>
