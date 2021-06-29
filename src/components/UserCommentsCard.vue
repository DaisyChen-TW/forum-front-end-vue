<template>
  <div class="card">
    <div class="card-header"><strong>{{userProfile.Comments.length}}</strong> 已評論餐廳</div>
    <div class="card-body">
      <router-link v-for="Comment in userProfile.Comments" :key="Comment.id" :to="{ name:'restaurantShow', params: { id: Comment.id } }" >
        <img
          :src="Comment.Restaurant.image | emptyImage"
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