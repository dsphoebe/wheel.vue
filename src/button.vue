<template>
  <button
    class="w-button"
    :class="{[`icon-${iconPosition}`]: true}"
    @click="$emit('click')"
  >
    <w-icon v-if="icon && !loading" :name="icon" class="icon"></w-icon>
    <w-icon v-if="loading" name="loading" class="icon loading"></w-icon>
    <div class="content">
      <slot></slot>
    </div>
  </button>
</template>

<script>
import Icon from './icon'
export default {
  name: 'w-button',
  components: {
    'w-icon': Icon
  },
  props: {
    icon: {},
    loading: {
      type: Boolean,
      default: false
    },
    iconPosition: {
      type: String,
      default: 'left',
      validator (value) {
        return value === 'left' || value === 'right'
      }
    }
  }
}
</script>

<style lang="scss">
  @keyframes spin {
    0% {transform: rotate(0);}
    100% {transform: rotate(360deg);}
  }
  .w-button {
    color: var(--color);
    font-size: var(--font-size);
    height: var(--button-height);
    padding: 0 1em;
    border-radius: var(--border-radius);
    border: 1px solid var(--border-color);
    background: var(--button-bg);
    display: inline-flex;
    justify-content: center;
    align-items: center;
    vertical-align: middle;
    &:hover {
      border-color: var(--border-color-hover);
    }
    &:active {
      background-color: var(--button-active-bg)
    }
    &:focus {
      outline: none;
    }
    > .icon {
      order: 1;
      margin: 0 .3em 0 0;
      &.loading {
        animation: spin .8s linear infinite;
      }
    }
    > .content {
      order: 2;
    }
    &.icon-right {
      > .icon {
        order: 2;
        margin: 0 0 0 .3em;
      }
      > .content {
        order: 1;
      }
    }
  }
</style>
