<template>
  <div class="about-page">
    <!-- 1. 英雄式页眉 -->
    <div class="hero-section">
      <div class="hero-overlay"></div>
      <div class="hero-content">
        <h1>关于我们</h1>
        <p>探索智能计算与生命科学的无限可能</p>
      </div>
    </div>

    <div class="main-content">
      <!-- 2. 实验室简介，带滚动动画 -->
      <div class="about-section lab-intro" v-scroll-fade-in>
        <div class="image-container">
          <img :src="labLogo" alt="实验室 Logo" class="section-image logo-image" />
        </div>
        <div class="text-container">
          <h2>实验室简介</h2>
          <p>
            BioAI-Y(Ying's)o(Omics)u(United)th (thoughtful)-lab |
            AI生物组学启智学实验室致力于前沿人工智能算法与多学科领域的交叉融合研究。实验室以智能计算为核心，专注于解决生物医学、健康医疗及生物信息学中的复杂数据分析与建模挑战。
          </p>
          <p>
            我们力求通过算法创新推动跨学科研究的突破，开发具备高泛化能力的通用分析工具与智能系统，旨在将数据价值转化为精准洞察，服务于科学研究与社会发展。
          </p>
        </div>
      </div>

      <!-- 3. 负责人简介，交错布局，带滚动动画 -->
      <div class="about-section professor-intro" v-scroll-fade-in="100">
        <div class="text-container">
          <h2>负责人简介</h2>
          <p>
            王颖教授，厦门大学自动化系教授、博士生导师，现任厦门市大数据智能决策与分析重点实验室主任。
          </p>
          <p>
            她于1995年进入中国科学技术大学自动化系学习，并于2002年获得模式识别与智能系统硕士学位。同年，她加入厦门大学自动化系，并于2007年获得控制理论与控制工程博士学位。
          </p>
        </div>
        <div class="image-container">
          <img :src="professorPhoto" alt="王颖教授照片" class="section-image professor-image" />
        </div>
      </div>

      <!-- 4. 科研成就部分，带滚动动画 -->
      <div class="achievements-section" v-scroll-fade-in="200">
        <h2>科研成果</h2>

        <!-- 科研项目 -->
        <div class="achievement-category">
          <div class="category-header">
            <h3>科研项目</h3>
          </div>
          <div class="achievement-list">
            <div
              v-for="(project, index) in achievements.researchProjects"
              :key="index"
              class="achievement-item"
            >
              <span class="achievement-number">{{ index + 1 }}</span>
              <span class="achievement-content">{{ project }}</span>
            </div>
          </div>
        </div>

        <!-- 教改项目 -->
        <div class="achievement-category">
          <div class="category-header">
            <h3>教改项目</h3>
          </div>
          <div class="achievement-list">
            <div
              v-for="(project, index) in achievements.educationalProjects"
              :key="index"
              class="achievement-item"
            >
              <span class="achievement-bullet">•</span>
              <span class="achievement-content">{{ project }}</span>
            </div>
          </div>
        </div>

        <!-- 发明专利 -->
        <div class="achievement-category">
          <div class="category-header">
            <h3>发明专利</h3>
          </div>
          <div class="achievement-list">
            <div
              v-for="(patent, index) in achievements.patents"
              :key="index"
              class="achievement-item"
            >
              <span class="achievement-number">{{ index + 1 }}</span>
              <span class="achievement-content">{{ patent }}</span>
            </div>
          </div>
        </div>

        <!-- 软件著作权 -->
        <div class="achievement-category">
          <div class="category-header">
            <h3>软件著作权</h3>
          </div>
          <div class="achievement-list">
            <div
              v-for="(copyright, index) in achievements.softwareCopyrights"
              :key="index"
              class="achievement-item"
            >
              <span class="achievement-number">{{ index + 1 }}</span>
              <span class="achievement-content">{{ copyright }}</span>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { onMounted, ref } from 'vue'
import labLogo from '@/assets/logo.png'
import professorPhoto from '@/assets/wangying.jpg'

// 科研成果数据
const achievements = ref({
  researchProjects: [
    '先验知识与时序数据融合的微生物群落动态特性系统表征，国家自然科学基金委员会, 面上项目',
    '福州市科技项目，对外科技合作项目，肿瘤患者肠菌移植疗法中微生物动态相关性智能跟踪与评估',
    '横向，数字营销决策大模型关键技术',
    '厦门市科技局，厦门市大数据智能分析与决策重点实验室项目',
    '国家自然科学基金委员会，面上项目，宏基因组数据的多尺度度量与多态相关性分析',
    '横向民机客舱乘员社会属性、心理及行为关系研究',
    '国家重点研发计划，鲍、螺抗逆及高产种质创制和规模化制种',
    '国家自然科学基金，高通量测序下微生物群落的比较、分析与理解',
    '国家自然科学基金，高通量 RNA-Seq 数据的偏差建模和差异表达基因识别',
  ],
  educationalProjects: [
    '2024年福建省课程思政教学团队负责人（《运筹学》）',
    '《互联网创业引导与实践》国家一流社会实践课程负责人',
    '主持福建省高等教育教学改革项目',
    '教育部高教司自动化教指委专业教育教学改革项目',
    '福建省高等学校创新创业教育自动化专业改革试点',
  ],
  patents: [
    '一种宏基组和宏转录组样本相异度的比较方法',
    '基于不同尺度tuple词频的微生物高通量测序数据分析协议',
    '一种基于k-tuple频度的核酸序列搜索方法及系统',
    '一种基于三元组神经网络的物种生物学分类方法及系统',
    '基于宏基因组的样本特异的物种互作网络构建方法及系统',
    '基于皮肤宏基因组数据的身份鉴定特征提取方法及系统',
    '一种标志基因识别的系统和方法，王颖，林仁豪',
    '一种基于ECG数据的高血压介导心脏损伤检测方法',
  ],
  softwareCopyrights: [
    'RNA-Seq数据分析工作流软件',
    '基因注解库的全面分析和完整评估软件',
    '基于物种相似性的基因组注解软件',
    '全基因组关联分析可视化集成平台',
    '基因组选择分析与育种可视化集成平台',
    '微生物作用关系网络构建系统',
  ],
})

// 自定义一个 Vue 指令来实现滚动触发动画
const vScrollFadeIn = {
  mounted: (el, binding) => {
    const delay = binding.value || 0
    const observer = new IntersectionObserver(
      (entries) => {
        entries.forEach((entry) => {
          if (entry.isIntersecting) {
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
.about-page {
  background-color: #f8f9fa; /* 柔和的背景色，增强学术感 */
}

/* --- Hero Section --- */
.hero-section {
  position: relative;
  height: 50vh;
  background-image: url('@/assets/media/about_us_bg.png');
  background-size: cover;
  background-position: center;
  background-attachment: fixed;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
  color: white;
}
.hero-content {
  position: relative;
  z-index: 1;
  max-width: 800px;
  padding: 0 20px;
}
.hero-content h1 {
  font-size: 3rem;
  font-weight: 600;
  margin-bottom: 15px;
}
.hero-content p {
  font-size: 1.3rem;
  margin-top: 10px;
  font-weight: 300;
  line-height: 1.6;
}

/* --- Main Content --- */
.main-content {
  max-width: 1100px;
  margin: -60px auto 60px; /* 让内容区向上移动，覆盖部分hero区域 */
  padding: 0 20px;
  position: relative;
  z-index: 2;
}

.about-section {
  display: grid;
  grid-template-columns: 1fr 2fr; /* 默认图片占1/3，文字占2/3 */
  gap: 50px;
  align-items: center;
  background: white;
  padding: 50px;
  border-radius: 8px;
  border-left: 4px solid #4b8f8b; /* 学术风格的左侧装饰线 */
  box-shadow: 0 6px 16px rgba(0, 0, 0, 0.06);
  margin-bottom: 40px;

  /* 动画初始状态 */
  opacity: 0;
  transform: translateY(30px);
  transition:
    opacity 0.8s ease-out,
    transform 0.8s ease-out;
}

/* 动画触发后的状态 */
.about-section.visible,
.achievements-section.visible {
  opacity: 1;
  transform: translateY(0);
}

.professor-intro {
  grid-template-columns: 2fr 1fr; /* 调整教授简介的布局 */
}

.image-container {
  text-align: center;
}
.section-image {
  max-width: 100%;
  height: auto;
}
.logo-image {
  max-width: 180px;
  border-radius: 4px;
}
.professor-image {
  border-radius: 50%;
  width: 200px;
  height: 200px;
  object-fit: cover;
  border: 3px solid #f8f9fa;
  box-shadow: 0 3px 10px rgba(0, 0, 0, 0.1);
}

.text-container h2 {
  font-size: 2rem;
  margin-bottom: 20px;
  font-weight: 600;
  color: #333;
  border-bottom: 2px solid #e9ecef;
  padding-bottom: 10px;
  display: inline-block;
}
.text-container p {
  font-size: 1.05rem;
  line-height: 1.8;
  color: #495057;
  margin-bottom: 15px;
}

/* --- 科研成就部分样式 --- */
.achievements-section {
  background: white;
  padding: 50px;
  border-radius: 8px;
  box-shadow: 0 6px 16px rgba(0, 0, 0, 0.06);
  opacity: 0;
  transform: translateY(30px);
  transition:
    opacity 0.8s ease-out,
    transform 0.8s ease-out;
}

.achievements-section h2 {
  font-size: 2.2rem;
  margin-bottom: 30px;
  font-weight: 600;
  color: #333;
  text-align: center;
  padding-bottom: 15px;
  border-bottom: 2px solid #4b8f8b;
  margin-bottom: 40px;
}

.achievement-category {
  margin-bottom: 40px;
}

.achievement-category:last-child {
  margin-bottom: 0;
}

.category-header {
  margin-bottom: 20px;
  padding-left: 10px;
  border-left: 3px solid #4b8f8b;
}

.category-header h3 {
  font-size: 1.5rem;
  font-weight: 600;
  color: #495057;
  margin-bottom: 10px;
}

.achievement-list {
  padding-left: 10px;
}

.achievement-item {
  display: flex;
  margin-bottom: 12px;
  line-height: 1.6;
  padding: 8px 0;
  border-bottom: 1px solid #f1f3f5;
}

.achievement-number {
  font-weight: 600;
  color: #4b8f8b;
  width: 30px;
  flex-shrink: 0;
  text-align: right;
  padding-right: 15px;
}

.achievement-bullet {
  color: #4b8f8b;
  font-weight: bold;
  margin-right: 15px;
  flex-shrink: 0;
}

.achievement-content {
  color: #495057;
  flex: 1;
  font-size: 1rem;
}

/* --- Responsive Design --- */
@media (max-width: 992px) {
  .about-section,
  .professor-intro {
    grid-template-columns: 1fr; /* 在平板上变为单列 */
    padding: 30px;
  }
  .professor-intro .image-container {
    order: -1; /* 在教授简介部分，将图片提到文字上方 */
  }
  .hero-content h1 {
    font-size: 2.5rem;
  }
  .hero-content p {
    font-size: 1.2rem;
  }
  .achievements-section {
    padding: 40px 30px;
  }
  .achievements-section h2 {
    font-size: 2rem;
  }
  .category-header h3 {
    font-size: 1.3rem;
  }
}

@media (max-width: 768px) {
  .main-content {
    margin-top: -40px;
  }
  .about-section,
  .professor-intro {
    padding: 25px;
  }
  .hero-content h1 {
    font-size: 2.2rem;
  }
  .hero-content p {
    font-size: 1.1rem;
  }
  .text-container h2 {
    font-size: 1.8rem;
  }
  .achievements-section {
    padding: 30px 20px;
  }
  .achievement-item {
    flex-direction: column;
  }
  .achievement-number,
  .achievement-bullet {
    margin-bottom: 5px;
    text-align: left;
    padding-right: 0;
  }
}

@media (max-width: 480px) {
  .hero-content h1 {
    font-size: 1.8rem;
  }
  .hero-content p {
    font-size: 1rem;
  }
  .text-container h2 {
    font-size: 1.6rem;
  }
  .achievements-section h2 {
    font-size: 1.8rem;
  }
  .about-section,
  .professor-intro,
  .achievements-section {
    padding: 20px;
  }
  .professor-image {
    width: 160px;
    height: 160px;
  }
}
</style>
