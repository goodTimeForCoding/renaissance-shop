<template>
  <footer class="footer">
    <div class="wrap">
      <div class="nav-wrap ">
        <NavComponent :isFooterNav="true"/>
      </div>
      <div class="contacts-wrap">
        <div class="contact-phone-wrap">
          <Phone />
          <a class="contact-phone" href="tel:+78125555555">+7(812)555-55-55</a>
        </div>
        <div class="contact-address">
          <Metka />
          <span class="contact address">г.Санкт-Петербург, ул. Ефимова, 3</span>
        </div>
      </div>
    </div>
  </footer>
</template>

<script>
import NavComponent from '@/components/NavComponent/index.vue';
import Phone from '@/components/Icons/Phone.vue';
import Metka from '@/components/Icons/Metka.vue';

export default {
  name: 'FooterComponent',
  components: { NavComponent, Phone, Metka },
};
</script>

<style lang="scss" scoped>
.footer {
  color: #555555;
  height: 96px;
  background-color: #ECEAEA;

  .wrap {
    margin: 0 auto;
    max-width: 1330px;
    padding: 0 10px;
    display: flex;
    justify-content: space-between;
    flex-wrap: wrap;
    gap: 20px;
  }

  .contacts-wrap {
    align-self: center;
    display: flex;
    flex-wrap: wrap;
    gap: 56px;
  }

  .nav-wrap {
    padding-left: 144px;

    @media (max-width: 1300px) {
      padding-left: 0px;
    }
  }

  .contact-phone-wrap,
  .contact-address {
    display: flex;
    align-items: center;
  }

  .contact-phone-wrap {
    gap: px;
    padding: 20px 0px;
  }

  .contact-phone-wrap a {
    text-decoration: none;
    color: #555555;
  }

  .contact-address {
    gap: 12px;
    padding: 20px 0px;
  }
}

@include tablet {
  .footer {
    height: auto;
    .wrap {
      gap: 20px;
      justify-content: center;
    }

    .nav-wrap {
      padding-left: 0px;
    }

    .contacts-wrap {
      gap: 20px;
    }
  }
}

@include mobile {
  .footer {
    height: auto;
    .wrap {
      gap: 20px;
      justify-content: center;
    }

    .nav-wrap {
      padding-left: 0px;
    }

    .footer__text {
      font-size: 12px;
    }

    .contacts-wrap {
      column-gap: 20px;
      row-gap: 5px;
    }
  }
}
</style>
