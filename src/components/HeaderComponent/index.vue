<template>
  <header class="header-nav">
    <nav class="nav-menu">
      <div class="nav-wrap">
        <NavComponent />
      </div>
      <div class="nav-search">
        <input class="nav-input" type="text" @input="updateSearch" :v-model="searchQuery"
          placeholder="Поиск по названию картины" />
        <button class="nav-button">Найти</button>
      </div>
    </nav>
  </header>
</template>

<script>
import NavComponent from '@/components/NavComponent/index.vue';

export default {
  name: 'HeaderComponent',
  components: { NavComponent },
  data() {
    return {
      searchQuery: '',
    };
  },
  methods: {
    updateSearch(event) {
      this.$emit('search', event.target.value);
    },
  },
};
</script>

<style lang="scss" scoped>
.header-nav {
  border-bottom: 1px solid #E1E1E1;

  .nav-menu {
    position: relative;
    margin: 0 auto;
    display: flex;
    gap: 20px;
    flex-wrap: wrap;
    justify-content: space-between;
    padding-left: 10px;
    padding-right: 10px;
    max-width: 1236px;
    align-items: center;
  }

  .nav-wrap {
    padding-left: 97px;
  }

  .nav-search {
    display: flex;
    align-items: center;
  }

  .nav-input {
    width: 294px;
    height: 48px;
    padding: 8px 15px;
    border: 1px solid #ccc;
  }

  .nav-input::placeholder {
    font-family: 'Merriweather';
    color: #9f9f9f;
    font-size: 14px;
  }

  .nav-button {
    width: 122px;
    height: 48px;
    padding: 8px 20px;
    background-color: #3a2e2e;
    color: white;
    border: none;
    cursor: pointer;
    transition: background 0.3s ease;
  }

  .nav-button:hover {
    background-color: #a52a2a;
  }
}

@include tablet {
  .header-nav {
    .nav-menu {
      flex-direction: column;
      gap: 5px;
      padding-bottom: 10px;

    }

    .nav-input,
    .nav-button {
      height: 35px;
    }

    .nav-wrap {
      padding-left: 0px;
    }
  }
}

@include mobile {
  .header-nav {
    .nav-menu {
      padding: 15px;
      display: block;
    }

    .nav-input,
    .nav-button {
      height: 40px;
    }

    .nav-button {
      width: 100px;
    }

    .nav-input {
      width: 100%;
    }

    .nav-wrap {
      padding-left: 0px;
      margin-bottom: 20px;
    }

    .nav-input::placeholder {
      font-size: 10px;
    }

    .nav-button {
      font-size: 12px;
    }
  }
}
</style>
