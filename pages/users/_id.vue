<template>
  <section class="container">
    <div>
      <h3>{{ user.id }}</h3>
      <img :src="user.profile_image_url" :alt="user.id" width="120">
      <p>{{ user.description || 'No description' }}</p>
      <p>
        <nuxt-link to="/" exact>
          <small>トップに戻る</small>
        </nuxt-link>
      </p>
      <h3>{{ user.name }}（@{{ user.id }}）さんの投稿一覧</h3>
      <ul>
        <li v-for="item in items" :key="item.id">
          <h4>{{ item.title }}</h4>
          <div>
            {{ item.body.slice(0, 130) }} ......
          </div>
          <p>
            <a :href="item.url" target="_blank" rel="noopener noreferrer">{{ item.url }}</a>
          </p>
        </li>
      </ul>
    </div>
  </section>
</template>

<script>
export default {
  head() {
    return {
      title: this.user.id
    }
  },
  async asyncData({ route, app }) {
    const user = await app.$axios.$get(`https://qiita.com/api/v2/users/${route.params.id}`)
    const items = await app.$axios.$get(`https://qiita.com/api/v2/items?query=user:${route.params.id}`)

    return { user, items }
  },
  async mounted() {

  },
}
</script>


<style scoped>
.container {
  min-height: 100vh;
  padding: 16px;
}

h3 {
  margin: 16px 0;
  padding: 8px 0;
  border-bottom: 1px solid #e5e5e5;
}

ul {
  margin: 2.5rem 1rem;
  padding: 0;
}

li + li {
  margin: 16px 0;
}

p {
  margin: 8px 0;
}

</style>
