<template>
  <div class="range-container">
    <div class="range-procent">{{ rangePlayer }}/{{ maxRange }}</div>
    <div class="range">
      <div class="range-fill" :style="{ width: (rangePlayer / maxRange) * 100 + '%' }"></div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    rangePlayer: {
      type: Number,
      required: true
    },
    maxRange: {
      type: Number,
      required: true
    }
  }
}
</script>

<style>
.range-container {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 5px;
  margin-top: 20px;
}
.range-procent {
  color: white;
}
.range {
  flex: 1;
  height: 20px;
  background: rgba(93, 1, 49, 0.5);
  border-radius: 10px;
  overflow: hidden;
  position: relative;
}
.range-fill {
  height: 100%;
  background: linear-gradient(
    90deg,
    rgba(93, 1, 49, 1) 0%,
    rgba(93, 0, 89, 1) 44%,
    rgba(255, 0, 99, 1) 100%
  );
  transition: width 0.3s ease;
}
</style>
