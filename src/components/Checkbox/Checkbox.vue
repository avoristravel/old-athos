<template>
    <div class="c-checkbox">
        <input
            :id="idElement"
            class="c-checkbox__input"
            :type="type"
            :name="name"
            :required="required"
            :disabled="disabled"
            :value="value"
            :checked="checked"
        >
        <label v-if="label" class="c-checkbox__label" :for="idElement">
            <span class="c-checkbox__label-text">
                {{ label }}
            </span>
        </label>
    </div>
</template>

<script>
    import formControl from '../../mixins/formControl'

    export default {
        name: 'AtCheckbox',
        mixins: [formControl],
        props: {
            type: {
                type: String,
                default: 'checkbox'
            }
        }
    }
</script>

<style lang="scss">
  .c-checkbox {
    $this: &;

    --c-checkbox-dimensions: 1em;
    --c-checkbox-font-size: 1em;
    --c-checkbox-input-border: #{em(1px)} solid #dfe0e4;
    --c-checkbox-input-background: #fff;
    --c-checkbox-input-radius: var(--radius-s);
    --c-checkbox-input-checked-background: #000;
    --c-checkbox-input-checked-border: #{em(1px)} solid #000;
    --c-checkbox-icon: 'I';
    --c-checkbox-align: center;

    display: flex;
    align-items: center;
    cursor: pointer;

    &__input {
      position: absolute;
      opacity: 0;

      &:checked {
        & + #{$this}__label {
          &::before {
            background: var(--c-checkbox-input-checked-background);
            border: var(--c-checkbox-input-checked-border);
            content: var(--c-checkbox-icon);
            font-family: var(--font-family-icons);
            color: #fff;
          }
        }
      }
    }

    &__label {
      display: flex;
      align-items: var(--c-checkbox-align);

      &::before {
        transition: all 0.3s;
        content: "";
        border: var(--c-checkbox-input-border);
        background: var(--c-checkbox-input-background);
        border-radius: var(--c-checkbox-input-radius);
        height: var(--c-checkbox-dimensions);
        width: var(--c-checkbox-dimensions);
        display: flex;
        align-items: center;
        justify-content: center;
        margin-right: 0.5em;
      }

      &-text {
        flex: 1;
        font-size: var(--c-checkbox-font-size);
      }
    }
  }
</style>
