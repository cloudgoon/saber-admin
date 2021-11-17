<template>
  <div class="avue-top">
    <!-- <div class="top-bar__left">
      <div
        class="avue-breadcrumb"
        :class="[{ 'avue-breadcrumb--active': isCollapse }]"
        v-if="showCollapse"
      >
        <i class="icon-navicon" @click="setCollapse"></i>
      </div>
    </div> -->

    <div class="top-bar__tags">
      <tags />
    </div>

    <div class="top-bar__right">
      <span class="column-splitline"></span>
      <el-tooltip
        v-if="showTheme"
        effect="dark"
        :content="$t('navbar.theme')"
        placement="bottom"
        class="tootip-none"
      >
        <div class="top-bar__item top-bar__item--show">
          <top-theme></top-theme>
        </div>
      </el-tooltip>
      <el-tooltip
        effect="dark"
        :content="$t('navbar.notice')"
        placement="bottom"
      >
        <div class="top-bar__item top-bar__item--show">
          <top-notice></top-notice>
        </div>
      </el-tooltip>

      <el-dropdown trigger="click">
        <div class="el-dropdown-link">
          <i class="iconfont iconwode2"></i>
          <i class="iconfont iconshushenglvehao"></i>
        </div>
        <el-dropdown-menu slot="dropdown">
          <el-dropdown-item>
            <router-link to="/">{{ $t('navbar.dashboard') }}</router-link>
          </el-dropdown-item>
          <el-dropdown-item>
            <router-link to="/info/index">
              {{ $t('navbar.userinfo') }}
            </router-link>
          </el-dropdown-item>
          <el-dropdown-item @click.native="logout" divided>
            {{ $t('navbar.logOut') }}
          </el-dropdown-item>
        </el-dropdown-menu>
      </el-dropdown>
    </div>
  </div>
</template>
<script>
import { resetRouter } from '@/router/router';
import { mapGetters, mapState } from 'vuex';
import { fullscreenToggel, listenfullscreen } from '@/util/util';
import tags from '../tags';

import topLock from './top-lock';
import topMenu from './top-menu';
import topSearch from './top-search';
import topTheme from './top-theme';
import topLogs from './top-logs';
import topColor from './top-color';
import topNotice from './top-notice';
import topLang from './top-lang';

export default {
  components: {
    topLock,
    topMenu,
    topSearch,
    topTheme,
    topLogs,
    topColor,
    topNotice,
    topLang,
    tags,
  },
  name: 'top',
  data() {
    return {};
  },
  filters: {},
  created() {},
  mounted() {
    listenfullscreen(this.setScreen);
  },
  computed: {
    ...mapState({
      showDebug: (state) => state.common.showDebug,
      showTheme: (state) => state.common.showTheme,
      showLock: (state) => state.common.showLock,
      showFullScren: (state) => state.common.showFullScren,
      showCollapse: (state) => state.common.showCollapse,
      showSearch: (state) => state.common.showSearch,
      showMenu: (state) => state.common.showMenu,
      showColor: (state) => state.common.showColor,
    }),
    ...mapGetters([
      'userInfo',
      'isFullScren',
      'tagWel',
      'tagList',
      'isCollapse',
      'tag',
      'logsLen',
      'logsFlag',
    ]),
  },
  methods: {
    handleScreen() {
      fullscreenToggel();
    },
    setCollapse() {
      this.$store.commit('SET_COLLAPSE');
    },
    setScreen() {
      this.$store.commit('SET_FULLSCREN');
    },
    logout() {
      this.$confirm(this.$t('logoutTip'), this.$t('tip'), {
        confirmButtonText: this.$t('submitText'),
        cancelButtonText: this.$t('cancelText'),
        type: 'warning',
      }).then(() => {
        this.$store.dispatch('LogOut').then(() => {
          resetRouter();
          this.$router.push({ path: '/login' });
        });
      });
    },
  },
};
</script>

<style lang="scss" scoped></style>
