<template>
  <header>
    <div class="p-header">
        <nav class="p-nav">
          <li
            v-for="(item, idx) in getNavTop"
            :key="idx"
            class="p-nav_item"
            @click="sliderIndicator(item.id)"
            :ref="'menu-item_' + item.id"
          >
            <NuxtLink :to="`${item.url}`" class="p-nav_item_link" @click="navigate(link.link)">
              {{ item.title }}
            </NuxtLink>
          </li>
          <div class="indicator" :style="{ left: positionToMove, width: sliderWidth }"></div>
        </nav>
      </div>
  </header>
</template>
<script>
export default {
  data() {
    return {
      sliderPosition: 0,
      selectedElementWidth: 0,
      selectedIndex: 0,
      getNavTop: getNavTop,
    }
  },
  computed: {
    positionToMove() {
      return this.sliderPosition + 'px'
    },
    sliderWidth() {
      return this.selectedElementWidth + 'px'
    },
    routerPath() {
      return this.$route.path
    },
  },
  methods: {
    sliderIndicator(id) {
      const el = this.$refs[`menu-item_${id}`][0]
      this.sliderPosition = el.offsetLeft
      this.selectedElementWidth = el.offsetWidth
      this.selectedIndex = id
    },
    navigate(path) {
      navigateTo({
        path,
      })
    },
  },
}
const getNavTop = [
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
header {
  position: relative;
}
.p-header {
  background: #fff;
  max-width: 1440px;
  margin: auto;
  padding: 20px 40px;
  padding-right: 56px;
  display: flex;
  align-items: center;
  height: 79px;
  justify-content: space-between;
}
.p-nav {
    list-style: none;
    display: flex;
    position: relative;
      align-items: center;
      gap: 32px;
  }
    .indicator {
      position: absolute;
      bottom: -32px;
      height: 4px;
      background-color: blue;
      transition: 0.3s ease-in-out;
    }
  .p-link {
    display: flex;
    align-items: center;
    gap: 32px;
    position: relative;
      display: grid;
      grid-auto-columns: 1fr;
      padding: 0 24px;
      gap: 24.5px;
  }
</style>
