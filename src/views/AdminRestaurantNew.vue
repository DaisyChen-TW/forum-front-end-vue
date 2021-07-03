<template>
  <div class="container py-5">
    <AdminRestaurantForm @after-submit="handleAfterSubmit" :is-processing="isProcessing" />
    
  </div>
</template>

<script>
import AdminRestaurantForm from './../components/AdminRestaurantForm.vue'
import adminAPI from './../apis/admin'
import { Toast } from './../utils/helpers'

export default {
  name: 'AdminRestaurantNew',
  components: {
    AdminRestaurantForm
  },
  data() {
    return {
      isProcessing: false
    }
  },
  methods: {
    async handleAfterSubmit (formData) {
      try{
      this.isProcessing = true
      // 透過 API 將表單資料送到伺服器
      const {data} = await adminAPI.restaurants.create({formData})
      if (data.status !== 'success') {
          throw new Error(data.message)
        }
      //跳頁面到admin-restaurants  
      this.$router.push({ name: 'admin-restaurants' })
      } catch (error) {
        this.isProcessing = false
        this.isLoading = false
        Toast.fire({
          icon: "error",
          title: "無法建立餐廳，請稍後再試",
        });
      }    
      
    }
  }
}
</script>