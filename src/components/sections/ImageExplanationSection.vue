<template>
  <div class="container">
    <div class="image-side">
      <div class="image-frame">
        <img :src="imageResized" :alt="imageAlt" class="image" draggable="false" />
      </div>
    </div>
    <div class="text-side">
      <div class="text">
        <slot name="content"></slot>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    imageSrc: {
      type: String,
      required: true
    },
    imageAlt: {
      type: String,
      required: true
    }
  },
  data() {
    return {
      screenWidth: window.innerWidth
    }
  },
  created() {
    window.addEventListener('resize', this.handleResize)
  },
  unmounted() {
    window.removeEventListener('resize', this.handleResize)
  },
  methods: {
    handleResize() {
      this.screenWidth = window.innerWidth
    }
  },
  computed: {
    imageResized() {
      if (this.screenWidth >= 1024) {
        return this.imageSrc + '.png'
      } else if (this.screenWidth >= 768) {
        return this.imageSrc + '-medium.png'
      } else {
        return this.imageSrc + '-small.png'
      }
    }
  }
}
</script>

<style lang="scss" scoped>
.container {
  display: flex;
  flex-direction: column;
  flex-wrap: wrap;
  min-height: 400px;
  width: 100%;
  background-color: #e4ecee;
}
.image-side {
  display: flex;
  flex: 50%;
  align-items: center;
  justify-content: center;
  padding: 30px 30px 0;
  // border: 1px solid red;
}
.image-frame {
  display: flex;
  justify-content: center;
  align-items: center;
  border-radius: 20px;
  overflow: hidden;
  background-color: #d9d9d9;
}
.image {
  user-select: none;
  display: flex;
  max-width: 100%;
  max-height: 100%;
}
.text-side {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  flex: 50%;
  padding: 30px;
  color: #181818;
  // border: 1px solid blue;
}

.text {
  max-width: 700px;
  text-align: center;
  font-size: 1rem;
}
</style>
