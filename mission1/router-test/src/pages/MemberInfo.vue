<template>
  <div className="mt-5">
    <img :src="member.photo" class="img" />
    <h4 class="mt-2">{{ member.name }} ({{ member.role }})</h4>
    <p>{{ member.desc }}</p>
    <a
      v-if="member.insta && member.insta !== ''"
      class="fa fa-instagram m-1"
      :href="member.insta"
    ></a>

    <a
      v-if="member.facebook && member.facebook !== ''"
      class="fa fa-facebook m-1"
      :href="member.facebook"
    ></a>

    <a
      v-if="member.youtube && member.youtube !== ''"
      class="fa fa-youtube m-1"
      :href="member.youtube"
    ></a>
    <br />
    <br />
    <router-link to="/members">멤버 목록으로</router-link>
  </div>
</template>

<script>
import { useRoute } from 'vue-router';
import members from '@/members.json';
export default {
  // 전달된 id를 꺼내서 id로 json 에서 개인  정보 검색 한 후
  // 개인정보 return 하면 template에 출력 가능
  name: 'MemberInfo',
  setup() {
    const currentRoute = useRoute();
    const id = parseInt(currentRoute.params.id, 10);
    const member = members.find((m) => m.id === id);
    return { member };
  },
};
</script>
