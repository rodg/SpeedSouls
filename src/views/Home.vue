<template>
  <div class="min-h-screen">
    <hero
      class="home min-h-screen md:min-h-0 shadow-md has-fixed-navbar"
      :style="style"
    >
      <SiteNotice />
      <div class="max-w-2xl md mx-auto text-center py-6 md:py-40">
        <img
          class="mx-auto mb-4"
          :src="require('@/assets/SpeedSouls-Horizontal-White_with_motto.png')"
          alt="speedsouls logo"
        />
        <div class="links py-5">
          <router-link
            class="btn -primary"
            tag="button"
            :to="{ name: 'Games' }"
          >
            <font-awesome-icon :icon="['fas', 'list']" />Leaderboards
          </router-link>
          <a :href="VUE_APP_WIKI" class="btn -primary">
            <font-awesome-icon :icon="['fas', 'angle-double-right']" />Future
            Wiki
          </a>
          <router-link
            class="btn -primary"
            tag="button"
            :to="{ name: 'Submit' }"
          >
            <font-awesome-icon :icon="['fas', 'hourglass-end']" />Submit a Run
          </router-link>
          <a :href="VUE_APP_DISCORD" class="btn -primary">
            <font-awesome-icon :icon="['fab', 'discord']" />Discord
          </a>
        </div>
      </div>
    </hero>
    <hero class="hero bg-nord5 text-nord0 dark:bg-nord0 dark:text-nord6">
      <div class="max-w-screen-md text-center mx-auto">
        <h1 class="text-4xl font-bold text-center py-0">About Us</h1>
        <p class="text-base py-8 text-center">
          Howdy. We're the DrakeNieR community. You like going fast? Our name
          ain't Sonic, but we do like our splits blue. Click that there link
          over yonder and get corralling the leaderboard today!
        </p>
      </div>
    </hero>
    <hero class="hero bg-nord4 text-nord0 dark:bg-nord1 dark:text-nord6">
      <div
        class="max-w-screen-md mx-auto flex flex-row items-center justify-evenly"
      >
        <div class="px-4 text-center">
          <h1 class="text-4xl font-bold text-center leading-none">
            Join The Community
          </h1>
          <p class="text-center py-8">
            Join our Discord server where over 1000 members are waiting for you!
            Ask questions and receive answers from veteran runners, and share
            your accomplishments and ideas with the community! Note however,
            that co-op requests and extensive casual discussions do not belong
            there. Do please choose a different Discord server for those topics.
          </p>

          <div class="flex flex-row px-2 py-2 justify-center">
            <discord />
          </div>
        </div>
      </div>
    </hero>
    <hero class="hero bg-nord5 text-nord0 dark:bg-nord2 dark:text-nord6">
      <div class="max-w-screen-md text-center mx-auto">
        <h1 class="text-4xl font-bold text-center py-0">Patreon</h1>
        <p class="text-base py-8 text-center">
          The source for this website came from SpeedSouls. They did most of the
          work. If you'd like to support them, a link to their patreon is below.
        </p>

        <div class="flex flex-row px-2 py-2 justify-center">
          <a :href="VUE_APP_PATREON" class="btn -primary">
            <font-awesome-icon class="mr-3" :icon="['fab', 'patreon']" />Open
            Patreon
          </a>
        </div>
      </div>
    </hero>
  </div>
</template>

<script>
const {
  VUE_APP_WIKI,
  VUE_APP_DISCORD,
  VUE_APP_GITHUB,
  VUE_APP_PATREON
} = process.env;

import SiteNotice from '@/components/SiteNotice';
import Hero from '@/components/Hero';
import Discord from '@/components/Discord';
import { computed, reactive, toRefs } from '@vue/composition-api';

export default {
  metaInfo: {
    title: 'DrakeNieR Speedruns',
    titleTemplate: null
  },
  components: { SiteNotice, Hero, Discord },
  setup(props, { root }) {
    const state = reactive({
      VUE_APP_WIKI,
      VUE_APP_GITHUB,
      VUE_APP_DISCORD,
      VUE_APP_PATREON,
      assets: [
        'na-1280',
        'nier-1280',
        'replicant-1280',
        'dod1_01',
        'dod1_02',
        'dod1_03',
        'dod2_01',
        'dod2_02',
        'dod3_01',
        'dod3_02',
        'na_01',
        'na_02',
        'ng_01',
        'ng_02',
        'nr_01',
        'nr_02'
      ]
    });

    const dark = computed(() => root.$store.getters.dark);
    const style = computed(() => {
      const image =
        state.assets[Math.floor(Math.random() * state.assets.length)];
      const url = require(`@/assets/backgrounds/${image}.jpg`);

      return {
        '--bg-url': `url(${url})`
      };
    });

    return {
      ...toRefs(state),
      dark,
      style
    };
  }
};
</script>

<style lang="scss" scoped>
.letter-spacing-px {
  letter-spacing: 1px;
}

.hero {
  @apply py-24;
}

.home {
  position: relative;
  overflow: hidden;

  .links {
    @apply flex;
    @apply flex-wrap;
    @apply flex-row;
    @apply justify-between;
    --gap: 10px;

    .btn {
      width: 100%;
      margin-bottom: var(--gap);

      svg {
        @apply mr-1;
      }

      @screen sm {
        width: calc(50% - (var(--gap) / 2));
      }
    }
  }

  &::before {
    content: '';
    background-color: black;
    position: absolute;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
    z-index: -11;
  }

  &::after {
    content: '';
    @apply opacity-75;
    transform: scale(1.1);
    background-image: var(--bg-url);
    background-repeat: no-repeat;
    background-size: cover;
    background-position: center;
    position: absolute;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
    z-index: -10;
  }
}
</style>
