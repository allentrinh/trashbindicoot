<template>
  <footer id="footer" class="footer section">
    <div class="container is-fluid">
      <div class="columns has-text-centered has-space-between is-vbottomed">
        <div class="column is-3 has-text-left-tablet">
          <router-link to="/" class="footer__logo">
            <img :src="require(`@/assets/TrashBindD07aR00a-A02.png`)" :alt="$store.state.title + ' Logo'" />
          </router-link>
          <SocialListComponent modifier="footer"/>
        </div>
        <div class="column is-3 has-text-right-tablet">
          <router-link to="contact" @click="this.logEvent('click', 'Footer Contact')" class="button button--ghost footer__button">Contact</router-link>
          <p class="footer__copyright">&copy; {{ year }} {{ $store.state.title }} - All Rights Reserved</p>
        </div>
      </div>
    </div>
  </footer>
</template>

<script>
import SocialListComponent from '@/components/SocialListComponent.vue';

export default {
  name: 'FooterComponent',
  components: {
    SocialListComponent,
  },
  computed: {
    year() {
      const date = new Date();
      return date.getFullYear();
    }
  }
};
</script>

<style lang="scss">
@import '@/assets/scss/styles.scss';

.has-space-between {
  justify-content: space-between;
}

.is-vbottomed {
  align-items: baseline;
}

.footer {
  background: #000;
  padding: 3rem 1.5rem;
  &__logo {
    display: inline-block;
    max-width: 150px;
    margin-bottom: 1rem;
  }
  &__button {
    margin-bottom: 1rem;
  }
  &__copyright {
    color: #fff;
  }
}
</style>
