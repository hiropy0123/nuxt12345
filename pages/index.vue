<template>
  <section class="container">
    <div>
      <h3>Nuxt.js のタグが付けられた投稿の一覧</h3>
      <ul>
        <li v-for="item in items" :key="item.id">
          <h4>
            <span>{{ item.title }}</span>
            <small>by {{ item.user.id }}</small>
          </h4>
          <div>{{ item.body.slice(0, 130) }} ......</div>
          <p>
            <a :href="item.url">{{ item.url }}</a>
          </p>
        </li>
      </ul>
    </div>
  </section>
</template>

<script>
export default {
  components: {
    
  },
  // async mounted() {
  //   console.log(
  //     JSON.stringify(await this.$axios.$get('https://qiita.com/api/v2/items?query=tag:nuxt.js'), true, ' ')
  //   )
  // },
  async asyncData({ app }) {
    const items = await app.$axios.$get('https://qiita.com/api/v2/items?query=tag:nuxt.js')

    return {
      items
    }
  }
}
</script>

<style>

.container {
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  max-width: 780px;
  margin: 5rem auto;
}

.title {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}

h3 {
  font-size: 28px;
  margin: 16px 0;
  padding: 8px 0;
  border-bottom: 1px solid #e5e5e5;
}

h4 {
  color: #0e1575;
  border-left: 5px solid currentColor;
  padding-left: 1rem;
  margin-bottom: 1rem;
}

ul {
  list-style: none;
}

li {
  border-bottom: 1px solid #e5e5e5;
  padding-bottom: 30px;
}
li + li {
  margin: 30px 0;
}

p {
  margin: 8px 0;
}
</style>
