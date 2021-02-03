<template>
  <div class="container pt-5">
    <div class="card">
      <h2>Актуальные новости {{ now }}</h2>
      <span>Открыто: {{ openRate }} | Прочитано {{ readRate  }}</span>
    </div>
    <app-news
      v-for="item in news"
      :key="item.id"
      :title="item.title"
      :id="item.id"
      :is-open="item.isOpen"
      :was-read="item.wasRead"
      @open-news="openNews"
      @read-news="readNews"
      @unmark="unReadNews"
    ></app-news>
  </div>
</template>

<script>
import AppNews from './AppNews'

export default {
  data () {
    return {
      now: new Date().toLocaleDateString(),
      news: [
        {
          title: 'Новость 1: America America',
          id: 1,
          isOpen: false,
          wasRead: false
        }, {
          title: 'Новость 2: Russia',
          id: 2,
          isOpen: false,
          wasRead: false
        }
      ],
      openRate: 0,
      readRate: 0
    }
  },
  components: {
    'app-news': AppNews
    // можно так зарегистрировать компонент
    // AppNews: AppNews
    // AppNews
  },
  provide () {
    return {
      title: 'Все новости:',
      news: this.news
    }
  },
  methods: {
    // можно передать параметр val из дочернего компонента
    openNews (data) {
      this.openRate++
      console.log(data)
    },
    readNews (id) {
      this.readRate++
      const idx = this.news.findIndex(news => news.id === id)
      this.news[idx].wasRead = true
    },
    unReadNews (id) {
      const news = this.news.find(news => news.id === id)
      news.wasRead = false
      this.readRate--
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
