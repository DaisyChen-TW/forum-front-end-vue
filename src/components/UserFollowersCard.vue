<template>
  <div class="card">
    <div class="card-header"><strong>{{userProfile.Followers.length}}</strong> followers (追隨者)</div>
    <div class="card-body">
      <router-link v-for="Follower in userProfile.Followers" :key="Follower.id" :to="{ name: 'user', params: { id: Follower.id }}">
        <img
          :src="Follower.image"
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