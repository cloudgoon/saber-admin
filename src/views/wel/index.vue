<template>
  <div class="firstPage">
    <img src="../../../public/img/6.png" width="381px" height="253px" alt="" />
  </div>
</template>

<script>
import { mapGetters } from 'vuex';

export default {
  name: 'wel',
  data() {
    return {
      activeNames: ['1', '2', '3', '5'],
      logActiveNames: ['24'],
    };
  },
  computed: {
    ...mapGetters(['userInfo']),
  },
  methods: {
    handleChange(val) {
      window.console.log(val);
    },
  },
};
</script>

<style>
.firstPage {
  display: flex;
  align-items: center;
  justify-content: center;
}
</style>
