// ./src/views/RestaurantsTop.vue
<template>
  <div class="container py-5">
    <NavTabs />
    <h1 class="mt-5">人氣餐廳</h1>
    <hr />
    <TopRestaurantCard
      v-for="restaurant in restaurants"
      :key="restaurant.id"
      :initial-restaurant="restaurant"
    />
  </div>
</template>
<script>
import NavTabs from "../components/NavTabs.vue";
import TopRestaurantCard from "../components/TopRestaurantCard.vue"
import restaurantsAPI from "./../apis/restaurants";
import { Toast } from "./../utils/helpers";

export default {
  components: {
    NavTabs,
    TopRestaurantCard
  },
  data () {
    return {
      restaurants: []
    }
  },
  created(){
    this.fetchTopRestaurants()
  },
  methods: {
    async fetchTopRestaurants () {
        try {
        const response = await restaurantsAPI.getTopRestaurants()
        const {restaurants} = response.data
        this.restaurants = restaurants
        }  catch (error) {
        Toast.fire({
          icon: "error",
          title: "無法取得TOP10人氣餐廳，請稍後再試",
        });
      }    
      
    }
  }
}
</script>