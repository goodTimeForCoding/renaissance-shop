<template>
  <div>
    <div class="painting-card"
    :class="{ 'card-disabled': getSoldStatus(painting.price) }" @click="openModal">
      <img class="painting-img"
      :src="require(`@/assets/images/${painting.img}`)" :alt="painting.title" />
      <div class="painting-info">
        <h3 class="title">{{ painting.title }}</h3>
        <p class="author">{{ painting.author }}</p>
        <div class="buy-wrap" @click.stop>
          <div class="price-wrap">
            <p class="old-price" v-if="painting.oldPrice">
              <s>{{ painting.oldPrice }}</s>
            </p>
            <p class="price">{{ painting.price }}</p>
          </div>
          <button class="buy-btn" :class="getIncartStatus" v-if="!getSoldStatus(painting.price)"
            @click="handlePurchase">
            <span v-if="status === 'default'">Купить</span>
            <span v-if="status === 'processing'" class="preloader-icon">
              <Spinner />
            </span>
            <span v-if="status === 'inCart'" class="checked-icon">
              <Check />В корзине
            </span>
          </button>
        </div>
      </div>
    </div>
    <CardModal :painting="painting" :isOpen="isModalOpen" @close="closeModal" />
  </div>
</template>

<script>
import Check from '@/components/Icons/Check.vue';
import Spinner from '@/components/Spinner/index.vue';
import CardModal from '@/components/CardModal/index.vue';

export default {
  name: 'PaintingCard',
  components: { Check, Spinner, CardModal },
  props: ['painting'],
  data() {
    return {
      status: this.getSavedStatus() || 'default',
      isModalOpen: false,
    };
  },
  methods: {
    handlePurchase() {
      if (this.status === 'default') {
        this.status = 'processing';
        setTimeout(() => {
          this.status = 'inCart';
          this.saveStatus();
        }, 2000);
      }
    },
    getSoldStatus(price) {
      if (price === 'Продана на аукционе') {
        return true;
      }
      return false;
    },
    saveStatus() {
      localStorage.setItem(`painting_${this.painting.id}_status`, this.status);
    },
    getSavedStatus() {
      return localStorage.getItem(`painting_${this.painting.id}_status`);
    },
    openModal() {
      this.isModalOpen = true;
    },
    closeModal() {
      this.isModalOpen = false;
    },
  },

  computed: {
    getIncartStatus() {
      return this.status === 'inCart' ? 'btn-incart' : '';
    },
  },
};
</script>

<style lang="scss" scoped>
.painting-card {
  width: 282px;
  height: 328px;
  color: #343030;
  border: 1px solid #E1E1E1;

  .painting-img {
    cursor: pointer;
  }

  .title {
    font-weight: 400;
    margin: 0;
    font-size: 18px;
    line-height: 150%;
    cursor: pointer;
  }

  .author {
    font-weight: 400;
    font-size: 18px;
    margin: 0;
    margin-bottom: 23px;
    cursor: pointer;
  }

  .buy-wrap {
    display: flex;
    gap: 10px;
    align-items: center;
    justify-content: space-between;
  }

  .painting-info {
    padding-top: 20px;
    padding-left: 24px;
    padding-right: 24px;
    padding-bottom: 24px;
  }

  .old-price {
    margin: 0;
    color: #A0A0A0;
    font-weight: 300;
    font-size: 14px;
  }

  .price {
    margin: 0;
    font-size: 16px;
    font-weight: 700;
    color: #343030;
  }

  .price-wrap {
    display: flex;
    flex-direction: column;
    gap: 3px;
  }

  .buy-btn {
    width: 118px;
    height: 48px;
    background-color: #382E2B;
    border: none;
    cursor: pointer;
    transition: background 0.3s ease;
    color: #F4F6F9;

    &:hover {
      background-color: #776763;
    }

    &:disabled {
      background-color: #C1B4B1;
    }
  }

  .btn-incart {
    background-color: #5B3A32;
    display: inline-flex;
    align-items: center;
    justify-content: center;
  }

  .preloader-icon {
    display: inline-flex;
    align-items: center;
    justify-content: center;
  }

  .checked-icon {
    display: flex;
    align-items: center;
    color: #F4F6F9;
    font-weight: bold;
    gap: 2px;
  }
}

.card-disabled {
  opacity: 0.5;
  .author {
    margin-bottom: 39px;
  }

  .painting-info {
    padding-top: 19px;
    padding-left: 25px;
    padding-right: 24px;
    padding-bottom: 24px;
  }
}

@include mobile {
  .painting-card {
    .title {
      font-size: 16px;
    }

    .author {
      font-size: 16px;
      margin-bottom: 10px;
    }
  }
}
</style>
