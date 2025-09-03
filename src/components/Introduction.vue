<template>
  <div class="intro-container">
    <!-- 1. 实验室简介，带滚动动画 -->
    <div class="intro-section lab-intro" v-scroll-fade-in>
      <div class="image-container">
        <img :src="labLogo" alt="实验室 Logo" class="section-image logo-image" />
      </div>
      <div class="text-container">
        <div class="section-header">
          <div class="section-icon">
            <svg
              width="24"
              height="24"
              viewBox="0 0 24 24"
              fill="none"
              xmlns="http://www.w3.org/2000/svg"
            >
              <path
                d="M21 15V5C21 3.89543 20.1046 3 19 3H5C3.89543 3 3 3.89543 3 5V15C3 16.1046 3.89543 17 5 17H21V15Z"
                stroke="#4b8f8b"
                stroke-width="2"
                stroke-linecap="round"
                stroke-linejoin="round"
              />
              <path
                d="M9 9H7C6.44772 9 6 9.44772 6 10V14C6 14.5523 6.44772 15 7 15H9"
                stroke="#4b8f8b"
                stroke-width="2"
                stroke-linecap="round"
                stroke-linejoin="round"
              />
              <path
                d="M17 9H15C14.4477 9 14 9.44772 14 10V14C14 14.5523 14.4477 15 15 15H17"
                stroke="#4b8f8b"
                stroke-width="2"
                stroke-linecap="round"
                stroke-linejoin="round"
              />
              <path
                d="M21 19H3"
                stroke="#4b8f8b"
                stroke-width="2"
                stroke-linecap="round"
                stroke-linejoin="round"
              />
            </svg>
          </div>
          <h2>实验室简介</h2>
        </div>
        <p class="section-text">
          BioAl-Youth-Lab | AI生物组学启智学实验室
          致力于前沿人工智能算法与多学科领域的交叉融合研究。实验室以智能计算为核心,专注于解决生物医学、健康医疗及生物信息学中的复杂数据分析与建模挑战。
        </p>
        <p class="section-text">
          我们力求通过算法创新推动跨学科研究的突破,开发具备高泛化能力的通用分析工具与智能系统,旨在将数据价值转化为精准洞察,服务于科学研究与社会发展。
        </p>
        <p class="section-text">
          实验室拥有一支充满活力的师资与学生队伍,包括王颖教授以及十余名在读博士和硕士研究生,形成了一个富有创造力与协作精神的学术共同体。
        </p>
      </div>
    </div>

    <!-- 2. 负责人简介，交错布局，带滚动动画 -->
    <div class="intro-section professor-intro" v-scroll-fade-in>
      <div class="text-container">
        <div class="section-header">
          <div class="section-icon">
            <svg
              width="24"
              height="24"
              viewBox="0 0 24 24"
              fill="none"
              xmlns="http://www.w3.org/2000/svg"
            >
              <path
                d="M19 21H5C3.89543 21 3 20.1046 3 19V12C3 10.8954 3.89543 10 5 10H19C20.1046 10 21 10.8954 21 12V19C21 20.1046 20.1046 21 19 21Z"
                stroke="#4b8f8b"
                stroke-width="2"
                stroke-linecap="round"
                stroke-linejoin="round"
              />
              <path
                d="M12 10C14.7614 10 17 7.76142 17 5C17 2.23858 14.7614 0 12 0C9.23858 0 7 2.23858 7 5C7 7.76142 9.23858 10 12 10Z"
                stroke="#4b8f8b"
                stroke-width="2"
                stroke-linecap="round"
                stroke-linejoin="round"
              />
            </svg>
          </div>
          <h2>负责人简介</h2>
        </div>
        <p class="section-text">
          王颖教授，厦门大学自动化系教授、博士生导师，现任厦门市大数据智能决策与分析重点实验室主任。
        </p>
        <p class="section-text">
          她于1995年进入中国科学技术大学自动化系学习，并于2002年获得模式识别与智能系统硕士学位。同年，她加入厦门大学自动化系，并于2007年获得控制理论与控制工程博士学位。
        </p>
        <div class="profile-links">
          <a href="#news" class="profile-link">研究方向</a>
          <a href="/publications" class="profile-link">发表论文</a>
          <a href="/contact" class="profile-link">联系我们</a>
        </div>
      </div>
      <div class="image-container">
        <img :src="professorPhoto" alt="王颖教授照片" class="section-image professor-image" />
      </div>
    </div>
  </div>
</template>

<script setup>
import { onMounted } from 'vue'
import labLogo from '@/assets/logo.png'
import professorPhoto from '@/assets/wangying.jpg'

// 自定义一个 Vue 指令来实现滚动触发动画
const vScrollFadeIn = {
  mounted: (el) => {
    const observer = new IntersectionObserver(
      (entries) => {
        entries.forEach((entry) => {
          if (entry.isIntersecting) {
            entry.target.classList.add('visible')
            observer.unobserve(entry.target) // 动画执行一次后停止观察
          }
        })
      },
      {
        threshold: 0.2, // 元素进入视口20%时触发
      },
    )
    observer.observe(el)
  },
}
</script>

<style scoped>
/* 容器样式 */
.intro-container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 60px 20px;
}

/* 简介部分通用样式 */
.intro-section {
  display: grid;
  grid-template-columns: 1fr 2fr; /* 默认图片占1/3，文字占2/3 */
  gap: 50px;
  align-items: center;
  background: white;
  padding: 50px;
  border-radius: 12px;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.08);
  margin-bottom: 50px;
  transition:
    transform 0.3s ease,
    box-shadow 0.3s ease;

  /* 动画初始状态 */
  opacity: 0;
  transform: translateY(40px);
  transition:
    opacity 0.8s ease-out,
    transform 0.8s ease-out;
}

/* 悬停效果 */
.intro-section:hover {
  transform: translateY(-5px);
  box-shadow: 0 15px 35px rgba(0, 0, 0, 0.1);
}

/* 动画触发后的状态 */
.intro-section.visible {
  opacity: 1;
  transform: translateY(0);
}

/* 教授简介的特殊布局 */
.professor-intro {
  grid-template-columns: 2fr 1fr; /* 调整教授简介的布局 */
}

/* 图片容器 */
.image-container {
  text-align: center;
}

/* 图片样式 */
.section-image {
  max-width: 100%;
  height: auto;
  border-radius: 8px;
  transition: transform 0.3s ease;
}

/* 实验室Logo样式 */
logo-image {
  max-width: 200px;
}

/* 教授照片样式 */
.professor-image {
  border-radius: 50%;
  width: 220px;
  height: 220px;
  object-fit: cover;
  border: 5px solid #fff;
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
}

/* 文字容器 */
.text-container {
  flex: 1;
}

/* 标题栏 */
.section-header {
  display: flex;
  align-items: center;
  margin-bottom: 25px;
}

/* 图标 */
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

/* 段落样式 */
.section-text {
  font-size: 1.1rem;
  line-height: 1.8;
  color: #555;
  margin-bottom: 20px;
  text-align: justify;
}

/* 链接容器 */
.profile-links {
  display: flex;
  gap: 15px;
  flex-wrap: wrap;
  margin-top: 25px;
}

/* 链接样式 */
.profile-link {
  display: inline-block;
  padding: 8px 20px;
  background-color: #f0f4f3;
  color: #4b8f8b;
  text-decoration: none;
  border-radius: 25px;
  font-weight: 500;
  transition: all 0.3s ease;
  border: 1px solid #e0e8e7;
}

/* 链接悬停效果 */
.profile-link:hover {
  background-color: #4b8f8b;
  color: white;
  transform: translateY(-2px);
  box-shadow: 0 4px 12px rgba(75, 143, 139, 0.3);
}

/* 响应式设计 */
@media (max-width: 992px) {
  .intro-section,
  .professor-intro {
    grid-template-columns: 1fr; /* 在平板上变为单列 */
    padding: 30px;
  }

  .professor-intro .image-container {
    order: -1; /* 在教授简介部分，将图片提到文字上方 */
  }

  .intro-section {
    margin-bottom: 40px;
    gap: 30px;
  }

  .section-header h2 {
    font-size: 2rem;
  }
}

@media (max-width: 768px) {
  .intro-container {
    padding: 40px 15px;
  }

  .intro-section {
    padding: 25px;
  }

  .section-header h2 {
    font-size: 1.8rem;
  }

  .section-text {
    font-size: 1rem;
  }

  .professor-image {
    width: 180px;
    height: 180px;
  }

  .profile-links {
    justify-content: center;
  }
}

@media (max-width: 480px) {
  .intro-container {
    padding: 30px 15px;
  }

  .intro-section {
    padding: 20px;
    gap: 25px;
  }

  .section-header h2 {
    font-size: 1.6rem;
  }

  .professor-image {
    width: 150px;
    height: 150px;
  }

  .section-text {
    font-size: 0.95rem;
  }

  .profile-link {
    padding: 6px 16px;
    font-size: 0.9rem;
  }
}
</style>
