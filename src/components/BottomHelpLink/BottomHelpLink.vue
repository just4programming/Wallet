<template lang="html">
  <div class="Bottom-help-link">
    <div v-if="type == 'issues'" class="issues">
      {{ $t('common.having-issues') }}
      <a
        href="https://howto.xinfin.org/XinFinWallet/features/"
        target="_blank"
        rel="noopener noreferrer"
        >{{ $t('common.help-center') }}</a
      >
    </div>
  </div>
</template>

<script>
export default {
  props: {
    type: {
      type: String,
      default: 'issues'
    }
  },
  data() {
    return {
      // Create a random string for each popover instance
      popOverId: 'popoverid' + String(Math.floor(Math.random() * 100000000))
    };
  }
};
</script>

<style lang="scss" scoped>
@import './BottomHelpLink';
</style>
