<template>
  <div class="news-section">
    <!-- 标题栏 -->
    <div class="section-header">
      <div class="header-left">
        <div class="section-icon">
          <svg
            width="24"
            height="24"
            viewBox="0 0 24 24"
            fill="none"
            xmlns="http://www.w3.org/2000/svg"
          >
            <path
              d="M12 21C16.9706 21 21 16.9706 21 12C21 7.02944 16.9706 3 12 3C7.02944 3 3 7.02944 3 12C3 16.9706 7.02944 21 12 21Z"
              stroke="#4b8f8b"
              stroke-width="2"
              stroke-linecap="round"
              stroke-linejoin="round"
            />
            <path
              d="M12 17V11"
              stroke="#4b8f8b"
              stroke-width="2"
              stroke-linecap="round"
              stroke-linejoin="round"
            />
            <path
              d="M12 7H12.01"
              stroke="#4b8f8b"
              stroke-width="2"
              stroke-linecap="round"
              stroke-linejoin="round"
            />
          </svg>
        </div>
        <h2>研究方向</h2>
      </div>
      <router-link to="/news" class="view-all-link"
        >查看全部 <span class="arrow-right">→</span></router-link
      >
    </div>

    <!-- 研究方向卡片网格，带滚动动画 -->
    <div class="news-grid">
      <div
        v-for="(news, index) in newsList"
        :key="news.id"
        class="news-card"
        v-scroll-fade-in="index"
      >
        <div class="card-image-container">
          <img :src="news.image" :alt="news.title" class="card-image" loading="lazy" />
          <div class="image-overlay">
            <div class="news-date">{{ news.date }}</div>
          </div>
        </div>
        <div class="card-content">
          <h3 class="card-title">{{ news.title }}</h3>
          <p class="card-summary">{{ news.summary }}</p>
          <div class="card-footer">
            <router-link :to="'/news/' + news.slug" class="learn-more-link"> 全部详情 </router-link>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { RouterLink } from 'vue-router'
import { newsItems } from '@/data/newsData.js'

// 使用项目数据文件中的研究方向数据
const newsList = ref(newsItems)

// 自定义一个 Vue 指令来实现滚动触发动画，并支持交错动画
const vScrollFadeIn = {
  mounted: (el, binding) => {
    const index = binding.value || 0
    const delay = index * 150 // 每张卡片延迟显示，创建交错效果

    const observer = new IntersectionObserver(
      (entries) => {
        entries.forEach((entry) => {
          if (entry.isIntersecting) {
            // 设置延迟，创建交错动画效果
            setTimeout(() => {
              entry.target.classList.add('visible')
              observer.unobserve(entry.target) // 动画执行一次后停止观察
            }, delay)
          }
        })
      },
      {
        threshold: 0.1, // 元素进入视口10%时触发
      },
    )
    observer.observe(el)
  },
}
</script>

<style scoped>
/* 研究方向部分容器 */
.news-section {
  max-width: 1200px;
  margin: 0 auto;
  padding: 60px 20px;
}

/* 标题栏样式 */
.section-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 40px;
  flex-wrap: wrap;
  gap: 20px;
}

.header-left {
  display: flex;
  align-items: center;
}

/* 图标样式 */
.section-icon {
  margin-right: 15px;
  color: #4b8f8b;
}

/* 标题样式 */
.section-header h2 {
  font-size: 2.2rem;
  font-weight: 600;
  color: #333;
  margin: 0;
}

/* 查看全部链接 */
.view-all-link {
  display: inline-flex;
  align-items: center;
  padding: 10px 24px;
  background-color: #4b8f8b;
  color: white;
  text-decoration: none;
  border-radius: 25px;
  font-weight: 500;
  font-size: 0.95rem;
  transition: all 0.3s ease;
  box-shadow: 0 4px 12px rgba(75, 143, 139, 0.2);
}

/* 箭头图标 */
.arrow-right {
  margin-left: 8px;
  font-size: 1rem;
  transition: transform 0.3s ease;
}

/* 查看全部链接悬停效果 */
.view-all-link:hover {
  background-color: #3a6b68;
  transform: translateY(-2px);
  box-shadow: 0 6px 16px rgba(75, 143, 139, 0.3);
}

.view-all-link:hover .arrow-right {
  transform: translateX(4px);
}

/* 研究方向卡片网格 */
.news-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(350px, 1fr));
  gap: 30px;
}

/* 研究方向卡片 */
.news-card {
  background: white;
  border-radius: 12px;
  overflow: hidden;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.05);
  transition: all 0.4s ease;
  display: flex;
  flex-direction: column;
  height: 100%;
  position: relative;
  overflow: hidden;
  z-index: 1;
  cursor: pointer;

  /* 动画初始状态 */
  opacity: 0;
  transform: translateY(30px);
}

/* 卡片动画触发后的状态 */
.news-card.visible {
  opacity: 1;
  transform: translateY(0);
}

/* 卡片悬停效果 */
.news-card:hover {
  transform: translateY(-8px);
  box-shadow: 0 15px 35px rgba(0, 0, 0, 0.1);
}

/* 卡片图片容器 */
.card-image-container {
  position: relative;
  height: 220px;
  overflow: hidden;
}

/* 卡片图片 */
.card-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.7s ease;
}

/* 图片悬停放大效果 */
.news-card:hover .card-image {
  transform: scale(1.08);
}

/* 图片覆盖层 */
.image-overlay {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  background: linear-gradient(to top, rgba(0, 0, 0, 0.7), transparent);
  padding: 15px 20px;
}

/* 日期样式 */
.news-date {
  color: white;
  font-size: 0.85rem;
  font-weight: 500;
  text-shadow: 0 1px 2px rgba(0, 0, 0, 0.5);
}

/* 卡片内容 */
.card-content {
  padding: 25px;
  flex: 1;
  display: flex;
  flex-direction: column;
}

/* 卡片标题 */
.card-title {
  font-size: 1.4rem;
  font-weight: 600;
  color: #333;
  margin-top: 0;
  margin-bottom: 15px;
  line-height: 1.4;
}

/* 卡片摘要 */
.card-summary {
  color: #555;
  line-height: 1.7;
  flex: 1;
  font-size: 1rem;
  margin-bottom: 20px;
}

/* 卡片底部 */
.card-footer {
  margin-top: auto;
}

/* 全部详情链接 */
.learn-more-link {
  display: inline-flex;
  align-items: center;
  color: #4b8f8b;
  text-decoration: none;
  font-weight: 600;
  font-size: 0.95rem;
  position: relative;
  transition: color 0.3s ease;
}

/* 全部详情链接悬停效果 */
.learn-more-link:hover {
  color: #3a6b68;
}

/* 链接下划线效果 */
.learn-more-link::after {
  content: '';
  position: absolute;
  bottom: -3px;
  left: 0;
  width: 0;
  height: 2px;
  background-color: #4b8f8b;
  transition: width 0.3s ease;
}

.learn-more-link:hover::after {
  width: 100%;
}

/* 响应式设计 */
@media (max-width: 992px) {
  .news-section {
    padding: 50px 20px;
  }

  .section-header {
    margin-bottom: 35px;
  }

  .section-header h2 {
    font-size: 2rem;
  }

  .news-grid {
    grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
    gap: 25px;
  }

  .card-image-container {
    height: 200px;
  }
}

@media (max-width: 768px) {
  .news-section {
    padding: 40px 15px;
  }

  .section-header {
    margin-bottom: 30px;
  }

  .section-header h2 {
    font-size: 1.8rem;
  }

  .view-all-link {
    padding: 8px 20px;
    font-size: 0.9rem;
  }

  .card-content {
    padding: 20px;
  }

  .card-title {
    font-size: 1.3rem;
  }
}

@media (max-width: 480px) {
  .news-section {
    padding: 30px 15px;
  }

  .section-header {
    flex-direction: column;
    align-items: flex-start;
    gap: 15px;
  }

  .section-header h2 {
    font-size: 1.6rem;
  }

  .news-grid {
    grid-template-columns: 1fr;
    gap: 20px;
  }

  .card-image-container {
    height: 180px;
  }

  .card-title {
    font-size: 1.2rem;
  }

  .card-summary {
    font-size: 0.95rem;
  }
}
</style>
