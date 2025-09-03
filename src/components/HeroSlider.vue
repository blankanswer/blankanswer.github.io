<template>
  <div class="hero-slider">
    <div class="slider-wrapper">
      <div
        v-for="(slide, index) in slides"
        :key="index"
        class="slide"
        :class="{ active: index === currentSlide }"
        :style="{ backgroundImage: `url(${slide.image})` }"
      >
        <div class="slide-overlay"></div>
        <div class="slide-content">
          <h1 class="slide-title">{{ slide.title }}</h1>
          <p class="slide-description">{{ slide.content }}</p>
        </div>
      </div>
    </div>

    <!-- 导航按钮 -->
    <button @click="prevSlide" class="nav-btn prev-btn">
      <svg
        width="24"
        height="24"
        viewBox="0 0 24 24"
        fill="none"
        xmlns="http://www.w3.org/2000/svg"
      >
        <path
          d="M15 18L9 12L15 6"
          stroke="white"
          stroke-width="2"
          stroke-linecap="round"
          stroke-linejoin="round"
        />
      </svg>
    </button>
    <button @click="nextSlide" class="nav-btn next-btn">
      <svg
        width="24"
        height="24"
        viewBox="0 0 24 24"
        fill="none"
        xmlns="http://www.w3.org/2000/svg"
      >
        <path
          d="M9 18L15 12L9 6"
          stroke="white"
          stroke-width="2"
          stroke-linecap="round"
          stroke-linejoin="round"
        />
      </svg>
    </button>

    <!-- 指示器 -->
    <div class="slide-indicators">
      <button
        v-for="(slide, index) in slides"
        :key="index"
        @click="goToSlide(index)"
        :class="{ active: index === currentSlide }"
        class="indicator"
        aria-label="Go to slide {{ index + 1 }}"
      ></button>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import welcomeImg from '@/assets/media/welcome.jpg'
import welcome2 from '@/assets/media/welcome2.jpg'
import welcome3 from '@/assets/media/welcome3.jpg'
import welcome4 from '@/assets/media/welcome4.jpg'

const currentSlide = ref(0)
let slideInterval = null
let isTransitioning = false

const slides = ref([
  {
    title: '欢迎来到我们的实验室',
    content:
      'BioAl-Youth-Lab | AI生物组学启智学实验室致力于前沿人工智能算法与多学科领域的交叉融合研究',
    image: welcomeImg,
  },
  {
    title: '团建活动',
    content: '一次愉快的植物园之旅，增进团队凝聚力与协作精神',
    image: welcome3,
  },
  {
    title: '项目合作',
    content: '与行业 partner 合作，共同推动 AI 技术在生物领域的应用',
    image: welcome4,
  },
])

// 下一张幻灯片
const nextSlide = () => {
  if (!isTransitioning) {
    isTransitioning = true
    setTimeout(() => {
      currentSlide.value = (currentSlide.value + 1) % slides.value.length
      isTransitioning = false
    }, 300)
  }
}

// 上一张幻灯片
const prevSlide = () => {
  if (!isTransitioning) {
    isTransitioning = true
    setTimeout(() => {
      currentSlide.value = (currentSlide.value - 1 + slides.value.length) % slides.value.length
      isTransitioning = false
    }, 300)
  }
}

// 跳转到指定幻灯片
const goToSlide = (index) => {
  if (!isTransitioning && index !== currentSlide.value) {
    isTransitioning = true
    setTimeout(() => {
      currentSlide.value = index
      isTransitioning = false
    }, 300)
  }
}

// 自动轮播
onMounted(() => {
  slideInterval = setInterval(nextSlide, 6000) // 自动轮播，6秒切换一次
})

// 清除轮播定时器
onUnmounted(() => {
  if (slideInterval) {
    clearInterval(slideInterval)
  }
})
</script>

<style scoped>
/* 英雄轮播容器 */
.hero-slider {
  position: relative;
  width: 100%;
  height: 80vh;
  overflow: hidden;
}

/* 轮播包装器 */
.slider-wrapper {
  width: 100%;
  height: 100%;
  position: relative;
}

/* 幻灯片 */
.slide {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-size: cover;
  background-position: center;
  background-attachment: fixed;
  opacity: 0;
  transition: opacity 0.8s ease-in-out;
  display: flex;
  justify-content: center;
  align-items: center;
}

/* 当前活动的幻灯片 */
.slide.active {
  opacity: 1;
  z-index: 1;
}

/* 幻灯片叠加层 */
.slide-overlay {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.4);
}

/* 幻灯片内容 */
.slide-content {
  position: relative;
  z-index: 2;
  text-align: center;
  color: white;
  max-width: 1000px;
  padding: 0 20px;
  transform: translateY(20px);
  opacity: 0;
  animation: fadeInUp 1s ease-out 0.3s forwards;
}

/* 标题动画 */
@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

/* 幻灯片标题 */
.slide-title {
  font-size: 3.5rem;
  font-weight: 700;
  margin-bottom: 20px;
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.5);
  line-height: 1.2;
}

/* 幻灯片描述 */
.slide-description {
  font-size: 1.2rem;
  line-height: 1.6;
  margin-bottom: 30px;
  font-weight: 300;
  text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.5);
}

/* 导航按钮 */
.nav-btn {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  width: 60px;
  height: 60px;
  background: rgba(255, 255, 255, 0.2);
  border: 2px solid rgba(255, 255, 255, 0.5);
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  transition: all 0.3s ease;
  z-index: 3;
  backdrop-filter: blur(5px);
}

/* 前一张按钮 */
.prev-btn {
  left: 30px;
}

/* 后一张按钮 */
.next-btn {
  right: 30px;
}

/* 按钮悬停效果 */
.nav-btn:hover {
  background: rgba(255, 255, 255, 0.3);
  transform: translateY(-50%) scale(1.1);
}

/* 指示器容器 */
.slide-indicators {
  position: absolute;
  bottom: 30px;
  left: 50%;
  transform: translateX(-50%);
  display: flex;
  gap: 10px;
  z-index: 3;
}

/* 指示器按钮 */
.indicator {
  width: 12px;
  height: 12px;
  border-radius: 50%;
  background: rgba(255, 255, 255, 0.5);
  border: none;
  cursor: pointer;
  transition: all 0.3s ease;
}

/* 活动的指示器 */
.indicator.active {
  width: 30px;
  border-radius: 6px;
  background: white;
}

/* 响应式设计 */
@media (max-width: 1200px) {
  .hero-slider {
    height: 70vh;
  }

  .slide-title {
    font-size: 3rem;
  }
}

@media (max-width: 992px) {
  .hero-slider {
    height: 60vh;
  }

  .slide-title {
    font-size: 2.5rem;
  }

  .slide-description {
    font-size: 1.1rem;
  }

  .nav-btn {
    width: 50px;
    height: 50px;
  }

  .prev-btn {
    left: 20px;
  }

  .next-btn {
    right: 20px;
  }
}

@media (max-width: 768px) {
  .hero-slider {
    height: 50vh;
  }

  .slide-title {
    font-size: 2rem;
  }

  .slide-description {
    font-size: 1rem;
  }

  .nav-btn {
    width: 40px;
    height: 40px;
  }

  .prev-btn {
    left: 15px;
  }

  .next-btn {
    right: 15px;
  }

  .slide-indicators {
    bottom: 20px;
  }
}

@media (max-width: 480px) {
  .hero-slider {
    height: 45vh;
  }

  .slide-title {
    font-size: 1.8rem;
  }

  .slide-description {
    font-size: 0.9rem;
    margin-bottom: 20px;
  }

  .nav-btn {
    width: 35px;
    height: 35px;
  }
}
</style>
