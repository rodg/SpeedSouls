<template>
  <div id="app" class="h-screen flex flex-col">
    <navbar
      class="absolute top-0 left-0 right-0 z-10"
      :class="{ 'dark:bg-gray-800': !isHome, 'bg-white': !isHome }"
      :transparant="isTransparant"
    />
    <main
      class="flex-grow z-0 bg-nord4 dark:bg-nord0"
      :class="{
        'has-fixed-navbar': !isHome
      }"
    >
      <keep-alive :include="['Home', 'Player', 'Run']">
        <router-view />
      </keep-alive>
    </main>
    <my-footer />
  </div>
</template>

<script>
import Navbar from '@/components/Navbar';
import MyFooter from '@/components/MyFooter';
import onEvent from '@/mixins/onEvent';
import { computed } from '@vue/composition-api';

export default {
  metaInfo: {
    title: 'DrakeNieR Speedruns',
    titleTemplate: '%s - DrakeNieR',
    meta: [
      {
        name: 'description',
        content:
          "Howdy. We're the DrakeNieR community. You like going fast? Our name ain't Sonic, but we do like our splits blue. Click that there link over yonder and get corralling the leaderboard today!"
      }
    ]
  },
  components: { Navbar, MyFooter },
  setup(props, { root }) {
    const isHome = computed(() => root.$route.name === 'Home');
    const isTransparant = computed(() => isHome.value);

    onEvent('focus', () => {
      if (root.$store.getters.theme === 'AUTO')
        root.$store.dispatch('enableAuto');
    });

    return {
      isHome,
      isTransparant
    };
  }
};
</script>

<style lang="scss">
@import '@/scss/main.scss';
</style>
