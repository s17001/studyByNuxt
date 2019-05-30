<template>
  <section class="container">
    <dev>
      <h3>{{user}}</h3>
      <img :src="user.profile_image_url" width="120" alt="">
      <p>{{user.description || 'No description'}}</p>
      <p>
        <nuxt-link to="/">
          <small><b>トップへ戻る</b></small>
        </nuxt-link>
      </p>
      <h3>{{user}}さんの投稿の一覧</h3>
      <ul>
        <li v-for="item in items" :key="item.id">
          <h4><span>{{item.title}}</span></h4>
          <div>{{item.body.slice(0,130)}}........</div>
          <p><a target="_blank" :href="item.url"></a></p>
        </li>
      </ul>
    </dev>
  </section>
</template>

<script>
  import {mapGetters} from 'vuex'

  export default {
    head () {
      return {
        title : this.user,
      }
    },
    async asyncData({ route, store , redirect }) {
      if (store.getters['users'][route.params.id]) {
        return
      }
      try {
        await store.dispatch('fetchUserInfo' , { id : route.params.id })
      } catch (e) {
        redirect('/')//404時にリダイレクト
      }
    },
    computed : {
      user () {
        return (this.users)[this.$route.params]
      },
      items () {
        return (this.userItems)[this.$route.params.id] || []
      },
      ...mapGetters(['users' , 'usersItems'])
    }
  }
</script>
