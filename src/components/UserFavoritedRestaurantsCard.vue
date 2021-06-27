<template>
  <div class="card">
    <div class="card-header"><strong>{{userProfile.FavoritedRestaurants.length}}</strong> 收藏的餐廳</div>
    <div class="card-body">
      <router-link v-for="FavoritedRestaurant in userProfile.FavoritedRestaurants" :key="FavoritedRestaurant.id" :to="{ name:'restaurantShow', params: { id: FavoritedRestaurant.id }}" >
        <img
          :src="FavoritedRestaurant.image"
          width="60"
          height="60"
          class="avatar"
        />
      </router-link>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    userProfile: {
      type: Object,
      require: true
    }  
  }
}
</script>