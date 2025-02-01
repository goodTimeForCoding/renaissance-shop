<template>
  <div v-if="isOpen" class="modal-overlay" @click.self="closeModal">
    <div class="modal-content">
      <button class="close-btn" @click="closeModal">&times;</button>
      <h2 class="title">{{ painting.title }}</h2>
      <p class="author">{{ painting.author }}</p>
      <Slider :images="painting.images" />
      <p class="description">{{ painting.description }}</p>
      <div class="price-wrap">
        <p class="price-text" v-if="!getSoldStatus()">Цена:</p>
        <div class="price-num">
          <p class="old-price" v-if="painting.oldPrice"><s>{{ painting.oldPrice }}</s></p>
          <p class="price">{{ painting.price }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Slider from '@/components/SliderComponent/index.vue';

export default {
  name: 'CardModal',
  components: { Slider },
  props: {
    painting: Object,
    isOpen: Boolean,
  },
  methods: {
    closeModal() {
      this.$emit('close');
    },
    getSoldStatus() {
      if (this.painting.price === 'Продана на аукционе') {
        return true;
      }
      return false;
    },
  },
};
</script>

<style lang="scss" scoped>
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 10;

  .title {
    padding: 0;
    margin: 0;
    font-size: 24px;
    font-weight: bold;
  }

  .author {
    padding: 0;
    margin: 10px 0px;
    font-size: 22px;
    font-weight: bold;
  }

  .description {
    font-size: 16px;
    line-height: 1.5;
    text-align: left;
  }

  .modal-content {
    position: relative;
    background: white;
    padding: 20px;
    border-radius: 8px;
    width: 800px;
    text-align: center;
  }

  .close-btn {
    position: absolute;
    top: -15px;
    right: 10px;
    background: none;
    border: none;
    font-size: 60px;
    cursor: pointer;
  }

  .slider img {
    width: 100%;
    height: auto;
    margin-bottom: 10px;
  }

  .price-wrap {
    margin-top: 5px;
    display: flex;
    justify-content: center;
    align-items: center;
    gap: 20px;
  }

  .price-text {
    font-size: 18px;
    font-weight: bold;
  }

  .old-price,
  .price {
    margin: 5px 0px;
    font-size: 18px;
    font-weight: bold;
  }
}

@include mobile {
  .modal-overlay {
    .modal-content {
      padding: 10px;
    }

    .description {
      font-size: 12px;
      text-align: left;
      margin-bottom: 0px;
    }

    .old-price,
    .price {
      margin: 2px 0px;
      font-size: 14px;
      font-weight: bold;
    }

    .price-text {
      font-size: 14px;
      font-weight: bold;
    }

    .title {
      font-size: 16px;
    }

    .author {
      padding: 0;
      margin: 5px 0px;
      font-size: 16px;
    }

    .close-btn {
      font-size: 55px;
    }
  }
}
</style>
