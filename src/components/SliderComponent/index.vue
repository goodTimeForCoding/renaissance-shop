<template>
  <div class="slider">
    <div class="slider-container"
    :style="{ transform: `translateX(-${currentIndex * 100}%)` }" @touchstart="startDrag"
      @touchmove="onDrag" @touchend="endDrag">
      <img v-for="(img, index) in images" :key="index"
      :src="require(`@/assets/images/${img}`)" alt="Painting image"
        class="slide" />
    </div>
    <button class="prev-btn" @click="prevSlide">&lt;</button>
    <button class="next-btn" @click="nextSlide">&gt;</button>

    <!-- Пагинация -->
    <div class="pagination">
      <span v-for="(img, index) in images" :key="index" class="pagination-dot"
        :class="{ active: index === currentIndex }" @click="goToSlide(index)"></span>
    </div>
  </div>
</template>

<script>
export default {
  name: 'SliderComponent',
  props: {
    images: {
      type: Array,
      required: true,
    },
  },
  data() {
    return {
      currentIndex: 0,
      isDragging: false,
      startPosX: 0,
      currentTranslate: 0,
      prevTranslate: 0,
    };
  },
  methods: {
    nextSlide() {
      this.currentIndex = (this.currentIndex + 1) % this.images.length;
    },
    prevSlide() {
      this.currentIndex = (this.currentIndex - 1 + this.images.length) % this.images.length;
    },
    startDrag(event) {
      this.isDragging = true;
      this.startPosX = this.getPositionX(event);
      this.prevTranslate = this.currentTranslate;
    },
    onDrag(event) {
      if (this.isDragging) {
        const currentX = this.getPositionX(event);
        this.currentTranslate = this.prevTranslate + currentX - this.startPosX;
      }
    },
    endDrag() {
      if (this.isDragging) {
        this.isDragging = false;
        const movedBy = this.currentTranslate - this.prevTranslate;

        // Если перемещение больше 100px, переключаем слайд
        if (movedBy < -50 && this.currentIndex < this.images.length - 1) {
          this.nextSlide();
        } else if (movedBy > 50 && this.currentIndex > 0) {
          this.prevSlide();
        }

        // Сбрасываем текущее смещение
        this.currentTranslate = -this.currentIndex * 100;
      }
    },
    getPositionX(event) {
      return event.type.includes('mouse') ? event.pageX : event.touches[0].clientX;
    },
    goToSlide(index) {
      this.currentIndex = index;
    },
  },
};
</script>

<style lang="scss" scoped>
.slider {
  position: relative;
  width: 100%;
  overflow: hidden;

  .slider-container {
    display: flex;
    transition: transform 0.5s ease;
  }

  .slide {
    min-width: 100%;
    height: auto;
    transition: transform 0.5s ease;
  }

  .prev-btn,
  .next-btn {
    font-size: 30px;
    position: absolute;
    top: 50%;
    transform: translateY(-50%);
    background: rgba(0, 0, 0, 0.5);
    color: white;
    border: none;
    padding: 10px;
    cursor: pointer;
    z-index: 10;
  }

  .prev-btn {
    left: 10px;
  }

  .next-btn {
    right: 10px;
  }

  /* Пагинация */
  .pagination {
    position: absolute;
    bottom: 10px;
    left: 50%;
    transform: translateX(-50%);
    display: flex;
    gap: 8px;
    z-index: 10;
  }

  .pagination-dot {
    width: 10px;
    height: 10px;
    background-color: rgba(255, 255, 255, 0.5);
    border-radius: 50%;
    cursor: pointer;
    transition: background-color 0.3s ease;
  }

  .pagination-dot.active {
    background-color: rgba(255, 255, 255, 1);
  }
}

@include mobile {
  .slider {
    .pagination-dot {
      width: 8px;
      height: 8px;
    }

    .prev-btn,
    .next-btn {
      display: none;
    }
  }
}
</style>
