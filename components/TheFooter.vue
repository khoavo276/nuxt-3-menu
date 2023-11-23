<template>
  <header>
    <div class="p-footer">
      <p>Menu footer ---></p>
        <nav class="p-navFooter">
          <li
            v-for="(item, idx) in getNavBottom"
            :key="idx"
            class="p-nav_item"
          >
            <NuxtLink :to="`${item.url}`" class="p-nav_item_link">
              {{ item.title }}
            </NuxtLink>
          </li>
        </nav>
      </div>
  </header>
</template>
<script>
export default {
  data() {
    return {
      getNavBottom: getNavBottom,
    }
  },
}
const getNavBottom = [
  {
    id: 1,
    url: '/',
    title: 'Home',
  },
  {
    id: 2,
    url: '/react',
    title: 'React',
  },
  {
    id: 3,
    url: '/angular',
    title: 'Angular',
  },
  {
    id: 4,
    url: '/vue',
    title: 'Vue',
  }
]
</script>
<style scoped>
.p-footer{
  padding: 20px;
}
.p-navFooter {
    display: flex;
    position: relative;
    align-items: center;
    gap: 32px;
    list-style: none;
  }
</style>
