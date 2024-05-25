<template>
  <div>
    <RangePower :range-player="rangePlayer" :max-range="maxRange" />
    <div
      class="game"
      @click="handleClick"
      :style="{ cursor: rangePlayer > 0 ? 'pointer' : 'not-allowed' }"
    >
      <div class="barabolya" :class="{ enlarge: isClicked }"></div>
      <transition-group name="coin">
        <span
          v-for="(coin, index) in coins"
          :key="index"
          class="number"
          :style="{ top: coin.y + 'px', left: coin.x + 'px' }"
          >+1</span
        >
      </transition-group>
    </div>
  </div>
</template>

<script>
import RangePower from './RangePower.vue'

export default {
  components: {
    RangePower
  },
  data() {
    return {
      coins: [],
      isClicked: false,
      rangePlayer: 100, // Початкове значення ренджа плеєра
      maxRange: 1500
    }
  },
  methods: {
    handleClick(event) {
      if (this.rangePlayer > 0) {
        const rect = event.currentTarget.getBoundingClientRect()
        const offsetX = event.clientX - rect.left - 40 // Adjusting for the size of the number element
        const offsetY = event.clientY - rect.top - 10

        this.coins.push({ x: offsetX, y: offsetY })
        this.isClicked = true
        this.rangePlayer -= 1 // Віднімаємо одиницю від ренджа плеєра

        setTimeout(() => {
          this.isClicked = false
          this.coins.shift()
        }, 1000) // Duration for the background scale effect
      }
    },
    incrementRangePlayer() {
      if (this.rangePlayer + 6 > this.maxRange) {
        this.rangePlayer = this.maxRange
      } else {
        this.rangePlayer += 6
      }
    }
  },
  mounted() {
    this.interval = setInterval(this.incrementRangePlayer, 3000)
  },
  beforeUnmount() {
    clearInterval(this.interval)
  }
}
</script>

<style>
.game {
  position: relative;
}

.barabolya {
  width: 100%;
  height: 90vh;
  background-image: url('@/assets/game/barabolya.png');
  background-size: contain;
  background-repeat: no-repeat;
  background-position: center center;
  cursor: pointer;
}

.number {
  position: absolute;
  font-size: 34px;
  font-weight: bold;
  color: white;
  animation: coinAnimation 0.3s forwards;
  user-select: none;
}

@keyframes coinAnimation {
  0% {
    transform: translateY(0) scale(1);
    opacity: 1;
  }
  50% {
    transform: translateY(-50px) scale(1.2);
    opacity: 1;
  }
  100% {
    transform: translateY(-100px) scale(1.5);
    opacity: 0;
  }
}

.coin-enter-active,
.coin-leave-active {
  transition:
    opacity 0.5s,
    transform 0.5s;
}
</style>
