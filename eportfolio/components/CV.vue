<template>
  <div class="timeline">
    <div
      v-for="(item, index) in timelineItems"
      :key="index"
      class="timeline-container"
      :class="index % 2 === 0 ? 'left-container' : 'right-container'"
    >
      <img :src="item.img" alt="test" />
      <div class="text-box">
        <h2>{{ item.title }}</h2>
        <p>
          <strong>{{ item.position }}</strong>
        </p>
        <small>{{ item.period }}</small>
        <p>{{ item.description }}</p>
        <span
          :class="
            index % 2 === 0 ? 'left-container-arrow' : 'right-container-arrow'
          "
        ></span>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import timelineData from '@/experience.json'

const timelineItems = ref([])

onMounted(() => {
  timelineItems.value = timelineData
})
</script>

<style scoped>
.timeline {
  position: relative;
  max-width: 1200px;
  margin: 100px auto;
}

.timeline-container {
  padding: 10px 50px;
  position: relative;
  width: 50%;
  animation: movedown 1s linear forwards;
  opacity: 0;
}

@keyframes movedown {
  0% {
    transform: translateY(-30px);
    opacity: 1;
  }
  100% {
    transform: translateY(0);
    opacity: 1;
  }
}

.timeline-container:nth-child(1) {
  animation-delay: 0s;
}

.timeline-container:nth-child(2) {
  animation-delay: 1s;
}

.timeline-container:nth-child(3) {
  animation-delay: 2s;
}

.text-box {
  padding: 20px 30px;
  background-color: aqua;
  position: relative;
  border-radius: 6px;
  font-size: 15px;
}

.left-container {
  left: 0;
}

.right-container {
  left: 84.3%;
}

.timeline-container img {
  position: absolute;
  width: 40px;
  border-radius: 50%;
  right: -20px;
  top: 32px;
  z-index: 10;
}

.right-container img {
  left: -20px;
}

.timeline:after {
  content: '';
  position: absolute;
  width: 6px;
  height: 100%;
  background: black;
  top: 0;
  left: 84.3%;
  margin-left: -3px;
  z-index: -1;
  animation: moveline 6s linear forwards;
}

@keyframes moveline {
  0% {
    height: 0;
  }
  100% {
    height: 100%;
  }
}

.text-box h2 {
  font-weight: 600;
}

.text-box small {
  display: inline-block;
  margin-bottom: 15px;
}

.left-container-arrow {
  height: 0;
  width: 0;
  position: absolute;
  top: 28px;
  z-index: 1;
  border-top: 15px solid transparent;
  border-bottom: 15px solid transparent;
  border-left: 15px solid green;
  right: -15px;
}

.right-container-arrow {
  height: 0;
  width: 0;
  position: absolute;
  top: 28px;
  z-index: 1;
  border-top: 15px solid transparent;
  border-bottom: 15px solid transparent;
  border-right: 15px solid green;
  left: -15px;
}

@media screen and (max-width: 600px) {
  .timeline {
    margin: 50px auto;
  }

  .timeline:after {
    left: 31px;
  }

  .timeline-container {
    width: 100%;
    padding-left: 80px;
    padding-right: 25px;
  }
  .text-box {
    font-size: 13px;
  }

  .text-box small {
    margin-bottom: 10px;
  }

  .right-container {
    left: 0;
  }

  .left-container img,
  .right-container img {
    left: 10px;
  }

  .left-container-arrow,
  .right-container-arrow {
    border-right: 15px solid green;
    border-left: 0;
    left: -15px;
  }
}
</style>
