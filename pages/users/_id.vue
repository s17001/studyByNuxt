<template>
  <section class="container">
    <dev>
      <h3>{{user.id}}</h3>
      <img :src="user.profile_image_url" width="120" alt="">
      <p>{{user.description || 'No description'}}</p>
      <p>
        <nuxt-link to="/">
          <small><b>トップへ戻る</b></small>
        </nuxt-link>
      </p>
      <h3>{{user.id}}さんの投稿の一覧</h3>
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
  export default {
    async asyncData({ route, app }) {
      const user = await app.$axios.$get(`https://qiita.com/api/v2/users/${route.params.id}`)
      const items = await app.$axios.$get(`https://qiita.com/api/v2/items?query=user:${route.params.id}`)

      return {user,items}
    }
  }
</script>
