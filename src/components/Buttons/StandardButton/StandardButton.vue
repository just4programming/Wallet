<template>
  <div
    :class="{
      'full-width': options.fullWidth,
      'mobile-full-width': options.mobileFullWidth,
      'hide-mobile-button': onBottomOfPage && options.isThisMobileBottomButton
    }"
    class="standard-button"
  >
    <div
      v-if="options.terms !== undefined && options.terms"
      class="accept-terms-Check-Box"
    >
      <check-box
        :terms="true"
        class="checkbox"
        @changeStatus="updateCheckbox($event)"
      />
    </div>
    <div :class="buttonClass">
      <button
        v-show="spinner"
        :disabled="diableButton"
        :class="[
          options.isThisMobileBottomButton ? 'mobile-bottom-button' : '',
          options.noMinWidth ? 'no-min-width' : '',
          options.paddingSmall ? 'padding-small' : ''
        ]"
        class="the-button-box"
      >
        <i class="fa fa-spin fa-spinner fa-lg" />
      </button>
      <button
        v-show="!spinner"
        :disabled="diableButton"
        :class="[
          options.isThisMobileBottomButton ? 'mobile-bottom-button' : '',
          options.noMinWidth ? 'no-min-width' : '',
          options.paddingSmall ? 'padding-small' : ''
        ]"
        class="the-button-box"
        @click.stop="clickFunction"
      >
        {{ options.title }}
        <i v-show="spinner" class="fa fa-spin fa-spinner fa-lg" />
        <img
          v-if="options.loadingIcon"
          :alt="$t('common.loading')"
          class="loading-left"
          src="@/assets/images/icons/loading.png"
        />

        <img
          v-if="options.rightArrow && options.buttonStyle == 'green'"
          :alt="$t('common.right-arrow')"
          class="arrow-right"
          src="@/assets/images/icons/arrow-right.svg"
        />

        <img
          v-if="options.rightArrow && options.buttonStyle == 'green-border'"
          :alt="$t('common.right-arrow')"
          class="arrow-right"
          src="@/assets/images/icons/arrow-right.svg"
        />

        <img
          v-if="options.leftArrow && options.buttonStyle == 'green'"
          :alt="$t('common.left-arrow')"
          class="arrow-left"
          src="@/assets/images/icons/arrow-left.svg"
        />

        <img
          v-if="options.leftArrow && options.buttonStyle == 'green-border'"
          :alt="$t('common.left-arrow')"
          class="arrow-left"
          src="@/assets/images/icons/arrow-green-left.svg"
        />
      </button>
    </div>
    <div v-if="options.customerSupport" class="customer-support-block">
      <customer-support />
    </div>
    <div v-if="options.helpCenter" class="help-center-block">
      <p>
        {{ $t('common.having-issues') }}
        <a
          href="https://howto.xinfin.org/XinFinWallet/features/"
          rel="noopener noreferrer"
          target="_blank"
          >{{ $t('common.help-center') }}</a
        >
      </p>
    </div>
  </div>
</template>

<script>
import CheckBox from '@/components/Buttons/CheckBox';
import CustomerSupport from '@/components/CustomerSupport';

export default {
  components: {
    'check-box': CheckBox,
    'customer-support': CustomerSupport
  },
  props: {
    options: {
      type: Object,
      default: function () {
        return {};
      }
    },
    buttonDisabled: {
      type: Boolean,
      default: false
    },
    spinner: {
      type: Boolean,
      default: false
    },
    clickFunction: {
      type: Function,
      default: function () {
        return;
      }
    }
  },
  data() {
    return {
      onBottomOfPage: false,
      termsAccepted: this.options.acceptTermsCheckBox
    };
  },
  computed: {
    diableButton() {
      if (this.options.terms !== undefined && this.options.terms) {
        return this.termsAccepted;
      }
      return this.buttonDisabled;
    },
    buttonClass() {
      switch (this.options.buttonStyle) {
        case 'white':
          return 'standard-button__white';
        case 'white-border':
          return 'standard-button__white-border';
        case 'grey':
          return 'standard-button__grey';
        case 'grey-border':
          return 'standard-button__grey-border';
        case 'red':
          return 'standard-button__red';
        case 'green':
          return 'standard-button__green';
        case 'green-border':
          return 'standard-button__green-border';
        case 'green-noclick':
          return 'standard-button__green-noclick';
        case 'green-transparent':
          return 'standard-button__green-transparent';
        case 'blue':
          return 'standard-button__blue';
        case 'blue-border':
          return 'standard-button__blue-border';
        default:
          return '';
      }
    }
  },
  beforeMount() {
    window.addEventListener('scroll', this.onPageScroll);
  },
  beforeDestroy() {
    window.removeEventListener('scroll', this.onPageScroll);
  },
  methods: {
    updateCheckbox(event) {
      this.termsAccepted = !event;
    },
    onPageScroll() {
      if (
        window.innerHeight + window.pageYOffset >=
        document.body.offsetHeight
      ) {
        this.onBottomOfPage = true;
      } else {
        this.onBottomOfPage = false;
      }
    }
  }
};
</script>

<style lang="scss" scoped>
@import 'StandardButton.scss';
</style>
