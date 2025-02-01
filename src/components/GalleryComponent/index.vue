<template>
  <section class="gallery-section">
    <h2 class="gallery-title">Картины эпохи Возрождения</h2>
    <div class="gallery" :class="{ 'gallery-filter': filteredPaintings.length <= 3 }">
      <PaintingCard v-for="painting in filteredPaintings" :key="painting.id" :painting="painting" />
    </div>
  </section>
</template>

<script>
import PaintingCard from '@/components/PaintingCard/index.vue';

export default {
  name: 'GalleryComponent',
  components: { PaintingCard },
  props: ['searchQuery'],
  data() {
    return {
      paintings: [
        {
          id: 1,
          title: '«Рождение Венеры»',
          author: 'Сандро Боттичелли',
          price: '1 000 000 $',
          oldPrice: '2 000 000 $',
          img: 'venera.png',
          images: ['venera.png', 'venera.png', 'venera.png', 'venera.png'],
          description: '"Рождение Венеры" — картина Сандро Боттичелли, написанная около 1484–1486 годов. Она изображает богиню Венеру, выходящую из морской пены на раковине, которая плывет к берегу. Справа её встречает богиня весны Флора, готовая укрыть Венеру покрывалом. Слева дуют Зефир и нимфа Хлорида, несущие ветер. Картина символизирует красоту, гармонию и пробуждение природы, отражая идеи эпохи Возрождения.',
        },
        {
          id: 2,
          title: '«Тайная вечеря»',
          author: 'Леонардо да Винчи',
          price: '3 000 000 $',
          img: 'vechera.png',
          images: ['vechera.png', 'vechera.png', 'vechera.png', 'vechera.png'],
          description: '"Тайная вечеря" — фреска Леонардо да Винчи, созданная в 1495–1498 годах в монастыре Санта-Мария-делле-Грацие в Милане. Она изображает момент, когда Иисус Христос объявляет ученикам, что один из них предаст его. Картина известна своими новаторскими композиционными решениями, реалистичностью выражений и глубокой перспективой. Центральная фигура — Христос, окруженный двенадцатью апостолами, чьи эмоции и жесты передают драматизм сцены.',
        },
        {
          id: 3,
          title: '«Сотворение Адама»',
          author: 'Микеланджело',
          price: '5 000 000 $',
          oldPrice: '6 000 000 $',
          img: 'adam.png',
          images: ['adam.png', 'adam.png', 'adam.png'],
          description: '"Сотворение Адама" — фреска Микеланджело, созданная около 1511 года на потолке Сикстинской капеллы в Ватикане. Она изображает момент, когда Бог дарует жизнь первому человеку, Адаму, прикосновением пальца. Фреска знаменита своей выразительной композицией, динамикой жестов и глубокой символикой, отражая идеи эпохи Возрождения о божественном происхождении человека.',
        },
        {
          id: 4,
          title: '«Урок анатомии»',
          author: 'Рембрандт',
          price: 'Продана на аукционе',
          img: 'rembrand.png',
          images: ['rembrand.png', 'rembrand.png'],
          description: '"Урок анатомии доктора Тульпа" — картина Рембрандта, написанная в 1632 году. Она изображает сцену, в которой группа врачей, во главе с доктором Тульпом, проводит публичное вскрытие тела преступника, казнённого на площади. Рембрандт мастерски передал не только точность анатомических деталей, но и психологическую атмосферу, показывая исследовательский процесс, внимательные взгляды врачей и реакцию зрителей. Картина считается шедевром реализма и одним из выдающихся произведений Золотого века Голландии.',
        },
      ],
    };
  },
  computed: {
    filteredPaintings() {
      return this.paintings.filter((painting) => {
        const searchLower = this.searchQuery.toLowerCase();
        return painting.title.toLowerCase().includes(searchLower);
      });
    },
  },
};
</script>

<style lang="scss" scoped>
.gallery-section {
  margin: 49px auto;
  padding-left: 10px;
  padding-right: 10px;
  max-width: 1236px;

  .gallery-title {
    margin: 0;
    font-size: 24px;
    font-weight: bold;
    margin-bottom: 39px;
    color: #343030;
  }

  .gallery {
    display: flex;
    justify-content: space-between;
    gap: 20px;
    flex-wrap: wrap;
  }

  .gallery-filter {
    justify-content: start;
  }
}

@include mobile {
  .gallery-section {
    margin-top: 30px;

    .gallery {
      gap: 20px;
      justify-content: center;
    }

    .gallery-title {
      font-size: 20px;
      text-align: center;
    }
  }
}
</style>
