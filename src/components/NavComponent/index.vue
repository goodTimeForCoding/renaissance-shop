<template>
  <div class="nav" :class="{ 'nav--closed': isNavClosed, 'nav--opened': isNavOpened }">
    <button v-if="!isFooterNav" class="button nav__toggle"
      @click="(isNavClosed = !isNavClosed), (isNavOpened = !isNavOpened)" type="button">
    </button>
    <ul class="nav__list" :class="{ 'nav__other': isFooterNav }">
      <li v-for="(item, index) in navItems" :key="index" class="nav-item">
        {{ item }}
      </li>
    </ul>
  </div>

</template>

<script>
export default {
  name: 'NavComponent',
  props: {
    isFooterNav: {
      type: Boolean,
      default: false,
    },
  },
  data() {
    return {
      isNavClosed: true,
      isNavOpened: false,
      navItems: ['Каталог', 'Доставка', 'Оплата', 'Контакты', 'О компании'],
    };
  },
};
</script>

<style lang="scss" scoped>
.nav {
  position: relative;

  &__toggle {
    position: relative;
    margin: 0;
    padding: 0;
    display: none;
    width: 48px;
    height: 48px;
    align-self: center;
    background-color: transparent;
    cursor: pointer;
    border: none;
    transition: background-color 0.3s ease;

    &:hover,
    &:active {
      background-color: #e0e2e6;
    }

    @include mobile {
      display: block;
    }
  }

  &__toggle::before {
    content: "";
    position: absolute;
    top: 12px;
    left: 6px;
    width: 36px;
    height: 4px;
    background-color: #9a9a9a;
    box-shadow: 0 10px 0 0 #9a9a9a, 0 20px 0 0 #9a9a9a;
  }

  &__toggle:active::before {
    background-color: #484848;
    box-shadow: 0 10px 0 0 #484848, 0 20px 0 0 #484848;
  }

  &__list {
    width: 542px;
    list-style: none;
    display: flex;
    gap: 20px;
    justify-content: space-between;
    padding: 0;
    margin: 0;
  }

  &--closed &__list {
    @include mobile {
      display: none;
    }
  }

  &--closed &__other {
    @include mobile {
      width: auto;
      list-style: none;
      display: flex;
      flex-wrap: wrap;
      column-gap: 20px;
      row-gap: 5px;
      justify-content: center;
      padding: 0;
      margin: 0;
      border-bottom: none;

      .nav-item {
        border-bottom: none;
      }
    }
  }

  &--opened &__list {
    @include mobile {
      display: block;
      width: 100%;
      text-align: center;
      position: relative;
      margin: 0;
      z-index: 2;
    }
  }

  &--opened &__toggle {
    top: 0;
    right: auto;
    left: 0;

    /*псевдоэлементы полосок крестика*/
    &::before,
    &::after {
      content: "";
      position: absolute;
      top: 21px;
      left: 6px;
      width: 36px;
      height: 4px;
      background-color: #9a9a9a;
    }

    /*поворачиваем одну из полосок на 45, другую на -45*/
    &::before {
      transform: rotate(45deg);
      box-shadow: none;
    }

    &::after {
      transform: rotate(-45deg);
    }

    &:active::before,
    &:active::after {
      background-color: #484848;
    }
  }

  .nav-item {
    padding-top: 38px;
    padding-bottom: 38px;
    cursor: pointer;
    transition: color 0.3s ease;
    white-space: nowrap;
  }

  .nav-item:hover {
    color: #a52a2a;
  }
}

@include tablet {
  .nav {
    .nav__list {
      width: auto;
      gap: 30px;
    }

    .nav-item {
      padding-top: 20px;
      padding-bottom: 20px;
    }
  }
}

@include mobile {
  .nav {
    .nav-item {
      padding-top: 15px;
      padding-bottom: 15px;
      border-bottom: 1px solid #3a2e2e;
    }
  }
}
</style>
