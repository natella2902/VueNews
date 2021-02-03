<template>
  <div>{{ title }}</div>
  <ul v-for="item in news" :key="item">
    <li>{{ item.title }}
      <span v-if="item.wasRead">!!!</span>
    </li>
  </ul>
</template>

<script>
export default {
  name: 'AppList',
  inject: ['title', 'news']
}
</script>

<style scoped>

</style>
