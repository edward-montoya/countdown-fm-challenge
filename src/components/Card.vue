<template>
  <article class="counterdown__time">
    <div class="counterdown__card">
      <div class="counterdown__digits counterdown__digits--superior">
        {{ padTwoDigits(props.value) }}
      </div>
      <div class="counterdown__digits counterdown__digits--inferior">
        {{ padTwoDigits(props.value) }}
      </div>
    </div>
    <h2 class="counterdown__unit">{{ props.label }}</h2>
  </article>
</template>

<script setup>
  import { padTwoDigits } from '../hooks/utils'

  let props = defineProps({
    value: {
      type: Number,
      required: true,
    },
    label: {
      type: String,
      required: true,
    },
  })
</script>

<style lang="scss" scoped>
  @import '../styles/mixins.scss';
  .counterdown {
    &__unit {
      font-size: var(--font-size-unit);
      text-align: center;
      letter-spacing: var(--countdown-letter-spacing);
      margin-top: 1rem;
      color: var(--grayish-blue);
    }
    &__card {
      @include size(var(--card-size), calc(var(--card-size) - 0.4rem));
      @include flex;
      border-radius: 4%;
      box-shadow: 0 0.8rem 0 0 hsl(234, 17%, 12%);
      position: relative;
      &::before,
      &::after {
        @include size(10px);
        content: '';
        display: block;
        position: absolute;
        top: 42%;
        border-radius: 50%;
        background-color: #282132;
        z-index: 1;
        overflow: hidden;
      }
      &::before {
        left: -6px;
      }
      &::after {
        right: -6px;
      }
    }
    &__digits {
      @include flex;
      @include absolute;
      color: var(--soft-red);
      font-size: var(--font-size-digits);
      border-radius: inherit;
      box-sizing: border-box;
      backface-visibility: hidden;
      transform-origin: center bottom;
      transform: rotateX(0) translate3d(0, 0, 0);
      transform-style: preserve-3d;
      -webkit-transform: translate3d(0, 0, 0);
      &--superior,
      &--inferior {
        width: 100%;
        height: 50%;
        overflow: hidden;
      }
      &--superior {
        border-bottom-left-radius: 0;
        border-bottom-right-radius: 0;
        top: 0;
        padding-top: 46%;
        background: #2a2b3c;
        &.flip {
          transform: rotateX(-180deg);
          transition: transform 1s cubic-bezier(0.8, 0.8, 0.375, 1.275);
        }
      }
      &--inferior {
        border-top-left-radius: 0;
        border-top-right-radius: 0;
        top: 50%;
        padding-bottom: 50%;
        background: var(--dark-desaturated-blue);
        transform-origin: center top;
      }
    }
  }

  @media screen and (min-width: 600px) {
    .counterdown {
      &__unit {
        margin-top: 1.8rem;
      }
      &__card {
        &::before,
        &::after {
          @include size(14px);
          top: 45%;
        }
      }
      &__digits {
        &--superior {
          padding-top: 48%;
        }
      }
    }
  }
</style>
