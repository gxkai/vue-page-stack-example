<template>
  <div class="c-home">
    <div class="h-body">
      <cube-tab-panels v-model="selectedIndex">
        <cube-tab-panel :label="$t('home')" value="0">
          <main-list></main-list>
        </cube-tab-panel>
        <cube-tab-panel :label="$t('about')" value="1">
          <about></about>
        </cube-tab-panel>
      </cube-tab-panels>
    </div>
    <div class="h-tabbars">
      <cube-tab-bar v-model="selectedIndex">
        <cube-tab v-for="(item) in tabs" :icon="item.icon" :label="item.label" :value="item.value" :key="item.value"></cube-tab>
      </cube-tab-bar>
    </div>
  </div>
</template>

<script>
import MainList from '@/views/main/MainList';
import About from '@/views/about/About';

export default {
  name: 'Home',
  components: { MainList, About },
  props: {},
  data() {
    return {
      selectedIndex: '0'
    };
  },
  computed: {
    tabs() {
      return [
        {
          value: '0',
          label: this.$t('home'),
          icon: 'iconfont ' + (this.selectedIndex === '0' ? 'iconhome_fill_light' : 'iconhome_light')
        },
        {
          value: '1',
          label: this.$t('about'),
          icon: 'iconfont ' + (this.selectedIndex === '1' ? 'iconmy_fill_light' : 'iconmy_light')
        }
      ];
    }
  },
  watch: {
    $route(to, from) {
      console.log('$route change');
    }
  },
  beforeRouteUpdate(to, from, next) {
    console.log('beforeRouteUpdate');
    this.selectedIndex = to.params.tab;
    next();
  },
  created() {
    console.log('Home created');
    this.selectedIndex = this.$route.params.tab || '0';
  },
  activated() {
    console.log('Home activated');
  },
  mounted() {},
  methods: {}
};
</script>

<style lang="scss">
.c-home {
  height: 100%;
  .h-body {
    height: calc(100% - 50px);
    .cube-tab-panels,
    .cube-tab-panels-group,
    .cube-tab-panel {
      height: 100%;
    }
    .cube-tab-panels-group {
      transition: none;
    }
  }
  .h-tabbars {
    height: 50px;
    .cube-tab-bar {
      border-top: 1px #9999994f solid;
      height: 100%;
      .cube-tab {
        height: 100%;
        display: flex;
        flex-direction: column;
        justify-content: space-around;
        i {
          font-size: 20px;
          margin-bottom: 3px;
        }
        &.cube-tab_active {
          color: $color-primary;
        }
      }
    }
  }
}
</style>
