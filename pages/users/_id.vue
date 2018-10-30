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
import { mapGetters } from 'vuex'

export default {
  head() {
    return {
      title: this.user.id
    }
  },
  async asyncData({ route, store, redirect }) {
    if ( store.getters['users'][route.params.id] ) {
      // ストアのusers[route.params.id] にすでにデータが格納されていれば、
      // 以下の処理は何もしない
      return
    }
    try {
      // actionsの'fetchUserInfo'を実行
      await store.dispatch('fetchUserInfo', { id: route.params.id })

    } catch(error) {
      // 簡易的なエラー処理として、404を想定してリダイレクト
      redirect('/')
    }
  },

  computed: {
    user() {
      return this.users[this.$route.params.id]
    },
    items() {
      return this.userItems[this.$route.params.id] || []
    },
    ...mapGetters(['users', 'userItems']),
    // ゲッターから'users'と'userItems'を取得
  }
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
