<template>
  <div class="contact-page">
    <div class="page-header">
      <h1>加入我们</h1>
      <p style="text-align: center">我们诚挚邀请对科研充满热情的您加入我们的团队</p>
    </div>

    <div class="container">
      <!-- 上部：招募信息 -->
      <div class="recruitment-section">
        <h2 class="section-title">人员招募</h2>
        <p class="recruitment-text">
          本实验室诚招研究生、推免研究生、博士生，以及本校有兴趣参与科研的本科生加入。我们期待与您一同探索科学前沿。
        </p>
        <div class="contact-details">
          <div class="info-item">
            <i class="fas fa-envelope-open-text"></i>
            <div>
              <strong>电子邮箱</strong>
              <p>wangying@xmu.edu.cn</p>
            </div>
          </div>
          <div class="info-item">
            <i class="fas fa-map-marked-alt"></i>
            <div>
              <strong>地址</strong>
              <p>福建省厦门市厦门大学翔安校区航空航天学院楼418室 (邮编: 361102)</p>
            </div>
          </div>
        </div>
      </div>

      <!-- 下部：地图 -->
      <div class="map-section">
        <h2 class="section-title">实验室位置</h2>
        <div class="map-container">
          <iframe
            width="100%"
            height="100%"
            frameborder="0"
            scrolling="no"
            marginheight="0"
            marginwidth="0"
            src="https://www.openstreetmap.org/export/embed.html?bbox=118.300,24.605,118.312,24.618&layer=mapnik&marker=24.61151,118.30585"
            style="border: 1px solid #ccc; border-radius: 8px"
          >
          </iframe>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
// No script logic needed for this static page
</script>

<style scoped>
.contact-page {
  padding-bottom: 50px;
}

.page-header {
  background: linear-gradient(45deg, #3a7bd5, #3a6073);
  color: white;
  text-align: center;

  padding: 60px 20px;
}
.page-header h1 {
  font-size: 3rem;
  margin: 0;
}
.page-header p {
  font-size: 1.2rem;
  opacity: 0.9;
}

.container {
  max-width: 900px;
  margin: 50px auto;
  padding: 0 20px;
}

.recruitment-section,
.map-section {
  padding: 40px;
  margin-bottom: 40px;
}

.section-title {
  text-align: center;
  font-size: 2.2rem;
  margin-bottom: 30px;
  color: #333;
}

.recruitment-text {
  font-size: 1.2rem;
  line-height: 1.8;
  text-align: center;
  color: #555;
  margin-bottom: 40px;
}

.contact-details {
  display: flex;
  flex-direction: column;
  gap: 20px;
}

.info-item {
  display: flex;
  align-items: flex-start;
  gap: 20px;
  font-size: 1.1rem;
}
.info-item i {
  color: #3a7bd5;
  font-size: 1.8rem;
  width: 30px;
  text-align: center;
  margin-top: 5px;
}
.info-item strong {
  display: block;
  color: #333;
  margin-bottom: 5px;
}
.info-item p {
  margin: 0;
  color: #666;
}

.map-container {
  height: 450px;
  border-radius: 8px;
  overflow: hidden;
}

/* Responsive adjustments */
@media (max-width: 768px) {
  .page-header h1 {
    font-size: 2.5rem;
  }
  .recruitment-section,
  .map-section {
    padding: 30px 20px;
  }
}
</style>
