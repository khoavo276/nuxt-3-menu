<template>
  <ul class="menu">
    <div
      class="menu-indicator"
      :style="{ left: positionToMove, width: sliderWidth }"
    ></div>
    <li
      class="menu-item"
      v-for="link in links"
      :key="link.id"
      @click="sliderIndicator(link.id)"
      :ref="'menu-item_' + link.id"
    >
      <a
        class="menu-link"
        :class="link.link === this.routerPath ? 'active' : null"
        @click="navigate(link.link)"
      >
        <i class="menu-icon" :class="link.icon"></i>
        <span>{{ link.text }}</span>
      </a>
    </li>
  </ul>
</template>

<script>
export default {
  data() {
    return {
      sliderPosition: 0,
      selectedElementWidth: 0,
      selectedIndex: 0,
      links: [
        {
          id: 1,
          icon: 'fab fa-react',
          text: 'React',
          link: '/react'
        },
        {
          id: 2,
          icon: 'fab fa-angular',
          text: 'Angular',
          link: '/angular'
        },
        {
          id: 3,
          icon: 'fab fa-vuejs',
          text: 'Vue',
          link: '/vue'
        }
      ]
    }
  },
  methods: {
    sliderIndicator(id) {
      let el = this.$refs[`menu-item_${id}`][0]
      this.sliderPosition = el.offsetLeft
      this.selectedElementWidth = el.offsetWidth
      this.selectedIndex = id
    },
    navigate(path) {
      navigateTo({
        path
      })
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
    }
  },
  mounted() {
    let currentMenuItem = this.links.find(
      ({ link }) => link === this.routerPath
    )
    if (currentMenuItem) {
      this.sliderIndicator(currentMenuItem.id)
    }
  }
}
</script>

<style>
:root {
  --active-color: #ffee93;
  --link-text-color: #f1faee;
  --menu-background-color: #1d3557;
  --active-background-color: #132238;
}
/* ul */
.menu {
  padding: 0;
  margin: 0;
  position: relative;
  background-color: var(--menu-background-color);
  display: inline-flex;
  border-radius: 4px;
  list-style-type: none;
  overflow: hidden;
}
/* li */
.menu-item {
  display: inline-flex;
}

/* a */
.menu-link {
  padding: 0.75rem 1rem;
  display: inline-flex;
  align-items: center;
  color: var(--link-text-color);
  text-decoration: none;
}

.menu-link:hover,
.menu-link.active {
  color: var(--active-color);
  background-color: var(--active-background-color);
}

/* icon */
.menu-icon {
  height: 1.5rem;
  width: 1.5rem;
  justify-content: center;
  align-items: center;
  display: inline-flex;
  margin-right: 0.2rem;
}
/* slider */
.menu-indicator {
  position: absolute;
  height: 0.25rem;
  background-color: var(--active-color);
  bottom: 0;
  left: 0;
  margin: auto;
  width: 3rem;
  transition: all ease 0.5s;
}
</style>
