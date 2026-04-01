<template>
  <div>
    <h2 class="m-4">이날치 멤버</h2>
    <div class="container">
      <div class="row">
        <!-- 한 가로 줄에 컬럼을 지정할 수 있음. 최대크기에는 6개, 중간에는 3~4개, 최소 2개 이상 설정 가능
         부스트트랩으로 가능 -->
        <div
          v-for="m in members"
          :key="m.id"
          class="col-6 col-xs-6 col-sm-4 col-md-3 col-lg-2"
        >
          {{ m.name }}
          <router-link :to="'/members/' + m.id">
            <img
              class="img-thumbnail"
              style="width: 90px; height: 110px"
              :src="m.photo"
              :title="m.name"
            /><br />
            <h6 class="display-7">{{ m.name }}</h6>
          </router-link>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import members from '@/members.json';

export default {
  name: 'Members',
  setup() {
    return { members };
  },
};
</script>
