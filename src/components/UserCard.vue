<template>
        <div class="col-3">
        <router-link :to="{ name: 'user', params: { id: user.id } }">
          <img
            :src="user.image | emptyImage"
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
            @click.stop.prevent="deleteFollowed(user.id)"
          >
            取消追蹤
          </button>
          <button 
            v-else
            type="button"
            class="btn btn-primary"
            @click.stop.prevent="addFollowed(user.id)"
          >
            追蹤
          </button>
        </p>
      </div>
</template>
<script>
import { emptyImageFilter } from "../utils/mixins";
import usersAPI from './../apis/users'
import { Toast } from './../utils/helpers'

export default {
  mixins: [emptyImageFilter],
  props: {
    initialUser: {
      type: Object,
      required: true
    }
  },
  data () {
    return {
      user: this.initialUser
    }
  },
  methods: {
    async deleteFollowed(userId) {
      try{
        const {data} = await usersAPI.deleteFollowed({userId})
        if (data.status !== 'success') {
        throw new Error(data.message)
        }
        this.user = {
        ...this.user,
        isFollowed: false,
        FollowerCount: this.user.FollowerCount - 1,
        }
      } catch (error) {
        Toast.fire({
          icon: "error",
          title: "無法取消追蹤，請稍後再試",
        });
        console.log("error", error);
      }
    },
    async addFollowed(userId) {
      try{
        const {data} = await usersAPI.addFollowed({userId})
        if (data.status !== 'success') {
        throw new Error(data.message)
        }
        this.user = {
        ...this.user,
        FollowerCount: this.user.FollowerCount + 1,
        isFollowed: true
        }
      } catch (error) {
        Toast.fire({
          icon: "error",
          title: "無法追蹤，請稍後再試",
        });
        console.log("error", error);
      }
    },
  }  
}
</script>


