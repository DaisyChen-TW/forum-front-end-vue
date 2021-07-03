<template>
  <div class="container py-5">
    <AdminRestaurantForm :initial-restaurant="restaurant" @after-submit="handleAfterSubmit" :is-processing="isProcessing" />
  </div>
</template>

<script>
import AdminRestaurantForm from "./../components/AdminRestaurantForm.vue";
import adminAPI from './../apis/admin'
import { Toast } from './../utils/helpers'

export default {
  components: {
    AdminRestaurantForm,
  },
  data() {
    return {
      restaurant: {
        id: -1,
        name: "",
        categoryId: "",
        tel: "",
        address: "",
        description: "",
        image: "",
        openingHours: "",
      },
      isProcessing: false
    };
  },
  created() {
    const { id } = this.$route.params;
    this.fetchRestaurant(id);
  },
  beforeRouteUpdate (to, from, next) {
    // 路由改變時重新抓取資料
    const { id } = to.params
    this.fetchRestaurant(id)
    next()
  },
  methods: {
    async handleAfterSubmit(formData) {
      try {
      this.isProcessing = true
      // 透過 API 將表單資料送到伺服器
      const {data} = await adminAPI.restaurants.update({restaurantId: this.restaurant.id, formData})
      if (data.status !== 'success') {
          throw new Error(data.message)
        }
      this.$router.push({ name: 'admin-restaurants' })
      } catch (error) {
        this.isProcessing = false
        this.isLoading = false
        Toast.fire({
          icon: "error",
          title: "無法修改餐廳資料，請稍後再試",
        });
      }
      
    },
    async fetchRestaurant(restaurantId) {
      try{
      this.isProcessing = false 
      const {data} = await adminAPI.restaurants.getDetail({restaurantId})
      console.log("fetchRestaurant id:", restaurantId);
      const { restaurant } = data;
      const { id, name, CategoryId: categoryId, tel, address, description, image, opening_hours: openingHours } = restaurant
      this.restaurant = {
        ...this.restaurant,
        id,
        name,
        categoryId,
        tel,
        address,
        description,
        image,
        openingHours
      };
      } catch (error) {
        this.isLoading = false
        this.isProcessing = false
        Toast.fire({
          icon: "error",
          title: "無法取得餐廳資料，請稍後再試",
        });
      }    
      
    },
  },
};
</script>