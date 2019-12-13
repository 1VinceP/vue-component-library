<script>
import { Spinner } from './index';

export default {
  name: 'base-button',

  components: { Spinner },

  props: {
    id: String,
    name: String,
    primary: Boolean,
    full: Boolean,
    lg: Boolean,
    sm: Boolean,
    green: Boolean,
    orange: Boolean,
    red: Boolean,
    isDelete: Boolean,
    disabled: Boolean,
    loading: Boolean,
  },
};
</script>

<template>
  <button
    :id="id"
    :name="name"
    :class="['button', { primary, full, lg, sm, green, orange, red, isDelete }]"
    @click="$emit('click', $event.target.name)"
    :disabled="disabled || loading"
  >
    <Spinner v-if="loading" />
    <slot v-else />
  </button>
</template>

<style lang="scss" scoped>
@import "/variables";

.button {
  height: 40px;
  background: transparent;
  display: flex;
  justify-content: center;
  align-items: center;
  border: none;
  border-radius: 3px;
  padding: 0 20px;
  color: $blue;
  font-size: 16px;
  cursor: pointer;
  &:active {
    background: $blue-faded;
  }
  &.primary {
    background: $blue;
    color: #fff;
    &:hover { background: #1ebdfc; }
    &:active { background: $blue; }
    &[disabled] {
      background: $grey;
      color: #fff;
    }
  }
  &.full {
    width: 100%;
  }
  &.lg {
    height: 46px;
    font-size: 18px;
  }
  &.sm {
    height: 30px;
    font-size: 14px;
  }
  &.green {
    background: $green;
    color: #fff;
    &:hover { background: lighten(#17AE82, 2%); }
    &:active { background: $green; }
    &[disabled] {
      background: $grey;
      color: #fff;
    }
  }
  &.orange {
    background: $orange;
    color: #fff;
    &:hover { background: #ff9100; }
    &:active { background: $orange; }
    &[disabled] {
      background: $grey;
      color: #fff;
    }
  }
  &.red {
    background: $red;
    color: #fff;
    &:hover { background: #db4256; }
    &:active { background: $red; }
    &[disabled] {
      background: $grey;
      color: #fff;
    }
  }
  &.isDelete {
    color: $red;
    font-size: 17px;
  }
  &[disabled] {
    color: $grey;
    cursor: default;
  }
}
</style>
