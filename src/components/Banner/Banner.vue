<template>
    <component
        :is="tag"
        :href="href && tag === 'a'"
        class="c-banner"
        :class="{
            'c-banner--has-shadow' : shadow,
            'c-banner--has-radius' : radius,
            'c-banner--has-overlay' : overlay
        }"
    >
        <AtPicture
            class="c-banner__picture"
            v-bind="picture"
        />
        <div
            v-if="$slots.default"
            class="c-banner__box"
            :class="{
                'c-banner__box--align-center' : align === 'center',
                'c-banner__box--align-right' : align === 'right',
                'c-banner__box--v-align-center' : valign === 'center',
                'c-banner__box--v-align-bottom' : valign === 'bottom'
            }"
        >
            <div class="c-banner__content">
                <slot />
            </div>
        </div>
    </component>
</template>

<script>
    import AtPicture from '../Picture/Picture.vue'

    export default {
        name: 'AtBanner',
        components: {
            AtPicture
        },
        props: {
            tag: {
                type: String,
                default: 'div'
            },
            href: {
                type: String,
                default: undefined
            },
            align: {
                type: String,
                default: undefined
            },
            valign: {
                type: String,
                default: undefined
            },
            shadow: {
                type: Boolean,
                default: false
            },
            radius: {
                type: Boolean,
                default: false
            },
            overlay: {
                type: Boolean,
                default: false
            },
            picture: {
                type: Object,
                default: () => {}
            }
        }
    }
</script>

<style lang="scss">
  .c-banner {
    $this: &;

    --c-banner-box-shadow: var(--shadow-distant);
    --c-banner-border-radius: var(--radius-s);
    --c-banner-overlay: transparent;
    --c-banner-picture-ratio-width: 13;
    --c-banner-picture-ratio-height: 17;
    --c-banner-content-padding: #{em(32px)};
    --c-banner-content-text-align: center;
    --c-banner-title-line-height: 1.4;
    --c-banner-title-font-size: #{em(26px)};
    --c-banner-title-color: #fff;
    --c-banner-title-text-align: center;
    --c-banner-button-margin-top: #{em(24px)};
    --c-banner-button-color: #fff;

    display: grid;
    grid-template-columns: 1fr;

    &--has-shadow {
      box-shadow: var(--c-banner-box-shadow);
    }

    &--has-radius {
      border-radius: var(--c-banner-border-radius);

      #{$this}__picture {
        border-radius: var(--c-banner-border-radius);
      }
    }

    &--has-overlay {
      #{$this}__picture {
        --c-picture-overlay: var(--c-banner-overlay);
      }
    }

    &__picture,
    &__box {
      position: relative;
      z-index: 1;
      grid-column: 1/2;
      grid-row: 1/2;
    }

    &__picture {
      --c-picture-ratio-width: var(--c-banner-picture-ratio-width);
      --c-picture-ratio-height: var(--c-banner-picture-ratio-height);
    }

    &__box {
      z-index: 3;
      min-width: #{em(1px)};

      &--v-align {
        &-center,
        &-bottom {
          display: flex;
          flex-direction: column;
          align-items: flex-start;
        }

        &-center {
          justify-content: center;
        }

        &-bottom {
          justify-content: flex-end;
        }
      }

      &--align {
        &-center,
        &-right {
          display: flex;
          flex-direction: column;
        }

        &-center {
          align-items: center;
        }

        &-right {
          align-items: flex-end;
        }
      }
    }

    &__content {
      text-align: var(--c-banner-content-text-align);
      max-width: 100%;
      padding: var(--c-banner-content-padding);
    }

    &__title {
      line-height: var(--c-banner-title-line-height);
      font-size: var(--c-banner-title-font-size);
      color: var(--c-banner-title-color);
      text-align: var(--c-banner-title-text-align);
      overflow: hidden;
      text-overflow: ellipsis;
    }

    &__button {
      color: var(--c-banner-button-color);
      margin-top: var(--c-banner-button-margin-top);
    }
  }
</style>
