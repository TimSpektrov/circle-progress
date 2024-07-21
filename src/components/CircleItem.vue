<template>
  <div class="circle-item">
    <div class="circle-item__number" :style="{'--rotate':`${350}deg`}">{{item.maxValue}}</div>
    <div class="circle-item__number" :style="{'--rotate':`${rotateTargetValue}deg`}">{{item.targetValue}}</div>
    <svg class="circle-item__progress" :style="{'--stroke-color': item.value < item.targetValue ? 'var(--cOrange)' : 'var(--cGreen)', '--stroke': percent < 100 ? percent : 106}">
      <circle cx="120" cy="120" r="100"></circle>
    </svg>
    <div class="circle-item__number" :style="{'--rotate':`${item.value < item.maxValue ? rotateValue : 350}deg`}">
      <div class="circle-item__number-completed">
        {{item.value}}
      </div>
    </div>
    <div class="circle-item__text-container">
      <div
        v-if="item.value < item.targetValue"
        class="circle-item__text"
      >
        Ещё продать<br /> на завтра <br />
        <span class="circle-item__text_accent circle-item__text_not-completed">+{{item.targetValue - item.value}}</span> ч
      </div>
      <div
        v-else
        class="circle-item__text"
      >
        <span class="circle-item__text_accent circle-item__text_completed">{{item.value}}</span> ч
      </div>
    </div>
  </div>
</template>

<script lang="ts">
export default {
  props: {
    item: {
      maxValue: {
        type: Number,
        required: true,
      },
      value: {
        type: Number,
        required: true,
      },
      targetValue: {
        type: Number,
        default: 0,
      },
    }
  },
  data() {
    return {
      rotateValue: 9 + (this.item.value / this.item.maxValue * 339),
      rotateTargetValue: 9 + (this.item.targetValue / this.item.maxValue * 339),
      percent: this.item.value / this.item.maxValue * 100
    }
  }
}
</script>

<style lang="scss">
  .circle-item {
    position: relative;
    width: 240px;
    height: 240px;
    border-radius: 50%;
    background-color: var(--cDark);

    &__text-container {
      position: absolute;
      top: 50%;
      left: 50%;
      width: 155px;
      height: 155px;
      display: flex;
      justify-content: center;
      align-items: center;
      padding: 24px;
      translate: -50% -50%;
      border-radius: 50%;
      background-color: var(--cBg);
    }
    &__text {
      color: #B5C3D7;
      font-size: 13px;
      line-height: 18px;
      font-family: var(--fPrimary);
      font-weight: 400;
      text-align: center;

      &_accent {
        font-family: var(--fSecondary);
        font-weight: 900;
        font-size: 38px;
        line-height: 53px;

      }
      &_not-completed {
        color: var(--cOrangeText);
      }
      &_completed {
        color: var(--cGreenText);
      }
    }
    &__number {
      position: absolute;
      top: 0;
      bottom: 0;
      left: 50%;
      padding-top: 6px;
      translate: -50% 0;
      rotate: 9deg;
      line-height: 29px;
      color: var(--cLight2);
      font-size: 13px;
      animation: rotateNumber 1s ease-out forwards;
      &-completed {
        width: 29px;
        height: 29px;
        display: flex;
        justify-content: center;
        align-items: center;
        border-radius: 50%;
        background-color: var(--cBg);
        rotate: calc(var(--rotate) * -1);
      }
    }
    &__bg {
      position: absolute;
      width: 100%;
      height: 100%;
      circle {
        width: 100%;
        height: 100%;
        stroke-width: 38;
        stroke: var(--cBg);
        stroke-linecap: round;
        stroke-dasharray: calc(314 * 2); /* Длина окружности круга */
        fill: none;
      }
    }
    &__progress {
      position: absolute;
      width: 100%;
      height: 100%;
      border-radius: 50%;

      circle {
        width: 100%;
        height: 100%;
        fill: none;
        stroke-width: 40;
        stroke: var(--stroke-color);
        stroke-linecap: round;
        stroke-dasharray: calc(314 * 2);
        stroke-dashoffset: calc(314 * 2);
        rotate: -80deg;
        transform-origin: center;
        animation: strokeFilled 1s ease-out forwards;
      }
    }
  }

  @keyframes rotateNumber {
    100% {
      rotate: var(--rotate)
    }
  }

  @keyframes strokeFilled {
    100% {
      stroke-dashoffset: calc(628px - ((628px - 38px) * var(--stroke) / 100))
    }
  }
</style>