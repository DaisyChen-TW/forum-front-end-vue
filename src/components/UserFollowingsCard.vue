<template>
  <div class="card">
    <div class="card-header"><strong>{{userProfile.Followings.length}}</strong> followings (追蹤者)</div>
    <div class="card-body">
      <router-link v-for="Following in userProfile.Followings" :key="Following.id" :to="{ name: 'user', params: { id: Following.id }}">
        <img
          :src="Following.image | emptyImage"
          width="60"
          height="60"
          class="avatar"
        />
      </router-link>
    </div>
  </div>
</template>
<script>
import { emptyImageFilter } from "../utils/mixins"
export default {
  mixins: [emptyImageFilter],
  props: {
    userProfile: {
      type: Object,
      require: true
    }  
  }
}
</script>