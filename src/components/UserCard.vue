<template>
        <div class="col-3">
        <router-link to="#">
          <img
            :src="user.image"
            width="140px"
            height="140px"
          >
        </router-link>
        <h4>{{user.name}}</h4>
        <span class="badge badge-secondary">追蹤人數：{{ user.FollowerCount }}</span>
        <p class="mt-3">
          <button v-if="user.isFollowed"
            type="button"
            class="btn btn-danger"
            @click.stop.prevent="deleteFollowed"
          >
            取消追蹤
          </button>
          <button 
            v-else
            type="button"
            class="btn btn-primary"
            @click.stop.prevent="addFollowed"
          >
            追蹤
          </button>
        </p>
      </div>
</template>
<script>
export default {
  props: {
    user: {
      type: Object,
      required: true
    }
  },
  data () {
    return {
      users: this.users
    }
  },
  methods: {
    deleteFollowed () {
      this.user = {
        ...this.user,
        isFollowed: false
      }
    },
    addFollowed () {
      this.user = {
        ...this.user,
        isFollowed: true
      }
    }
  }  
}
</script>
