<template>
    <label
        class="c-toggle-switch"
        :class="{'c-toggle-switch--disabled' : disabled}"
    >
        <input
            :id="idElement"
            class="c-toggle-switch__input"
            :type="type"
            :name="name"
            :required="required"
            :disabled="disabled"
            :value="value"
            :checked="checked"
        >
        <span class="c-toggle-switch__slider"></span>
        <span v-if="label" class="c-toggle-switch__text">
            {{ label }}
        </span>
    </label>
</template>

<script>
    import formControl from '../../mixins/formControl'

    export default {
        name: 'AtToggleSwitch',
        mixins: [formControl],
        props: {
            type: {
                type: String,
                default: 'checkbox'
            },
            disabled: {
                type: Boolean,
                default: false
            }
        }
    }
</script>

<style lang="scss">
  .c-toggle-switch {
    $this: &;

    --c-toggle-swith-width: 3em;
    --c-toggle-swith-height: 1.5em;
    --c-toggle-swith-slider-width: 1em;
    --c-toggle-swith-slider-height: 1em;
    --c-toggle-swith-slider-border: #{em(1px)} solid #888;
    --c-toggle-swith-slider-radius: 2em;
    --c-toggle-swith-slider-background: #ccc;
    --c-toggle-swith-slider-active-background: #000;
    --c-toggle-swith-slider-transform: #{em(4px)};
    --c-toggle-switch-text-font-size: 1em;
    --c-toggle-switch-text-padding-left: var(--c-toggle-swith-slider-width);

    position: relative;
    display: flex;
    align-items: center;
    width: var(--c-toggle-swith-width);
    height: var(--c-toggle-swith-height);

    &__input {
      opacity: 0;
      width: 0;
      height: 0;

      &:checked {
        & + #{$this}__slider {
          background: var(--c-toggle-swith-slider-active-background);

          &::before {
            transform: translateX(calc(100% + (var(--c-toggle-swith-slider-width) / 2) + (var(--c-toggle-swith-slider-transform) / 2)));
          }
        }
      }
    }

    &__text {
      padding-left: calc(var(--c-toggle-swith-width) + 0.5em);
      font-size: var(--c-toggle-switch-text-font-size);
    }

    &__slider {
      border: var(--c-toggle-swith-slider-border);
      position: absolute;
      cursor: pointer;
      top: 0;
      left: 0;
      right: 0;
      bottom: 0;
      background-color: var(--c-toggle-swith-slider-background);
      transition: 0.3s background;
      border-radius: var(--c-toggle-swith-slider-radius);

      &::before {
        position: absolute;
        content: "";
        height: var(--c-toggle-swith-slider-height);
        width: var(--c-toggle-swith-slider-width);
        transform: translateX(var(--c-toggle-swith-slider-transform));
        bottom: #{em(3px)};
        background-color: #fff;
        transition: 0.3s transform;
        border-radius: var(--radius-circle);
      }
    }

    &--disabled {
      opacity: 0.5;
      pointer-events: none;
    }
  }
</style>
