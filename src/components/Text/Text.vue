<template>
    <component
        :is="tag"
        :class="{'c-text--has-bg': background}"
        class="c-text"
    >
        <span class="c-text__text">
            {{ text }}
        </span>
    </component>
</template>

<style lang="scss">
  .c-text {
    --c-text-background: #c6c6c6;
    --c-text-padding: 0.5em;
    --c-text-color: currentColor;
    --c-text-font-size: 1em;
    --c-text-margin: 0;
    --c-text-line-height: 1.4;
    --c-text-font-weight: 400;

    color: var(--c-text-color);
    margin: var(--c-text-margin);

    &__text {
      font-weight: var(--c-text-font-weight);
      font-size: var(--c-text-font-size);
      line-height: var(--c-text-line-height);
    }

    &--has-bg {
      background: var(--c-text-background);
      padding: var(--c-text-padding);
    }
  }
</style>

<script>
    export default {
        name: 'AtText',
        props: {
            tag: {
                type: String,
                default: 'p'
            },
            background: {
                type: Boolean,
                default: false
            },
            text: {
                type: String,
                default: 'Lorem ipsum dolor sit amet'
            }
        }
    }
</script>
