<script setup lang="ts">
import { ref, onMounted } from 'vue'

// 精选内容数据 - 优化描述，符合项目实际情况
const heroContent = ref({
  title: '公路自行车百科与训练平台',
  subtitle: '专业 · 系统 · 科学',
  description: '构建完整的公路自行车知识体系，提供个性化AI训练计划，助力每位骑行者科学提升'
})

const featuredCategories = ref([
  {
    id: 'basics',
    title: '基础理论',
    subtitle: 'Fundamentals',
    description: '从零开始，构建完整的公路自行车知识体系，涵盖骑行基础、技术要领和安全知识',
    articleCount: 127,
    icon: 'book',
    color: 'blue'
  },
  {
    id: 'health',
    title: '运动科学',
    subtitle: 'Sports Science',
    description: '基于科学研究的训练方法与健康指导，包含生理学、营养学和康复知识',
    articleCount: 94,
    icon: 'activity',
    color: 'purple'
  },
  {
    id: 'equipment',
    title: '装备科学',
    subtitle: 'Equipment Science',
    description: '深度解析每一件装备的设计原理与选择标准，助您做出明智的装备决策',
    articleCount: 89,
    icon: 'settings',
    color: 'emerald'
  },
  {
    id: 'ai-training',
    title: 'AI训练计划',
    subtitle: 'AI Training',
    description: '个性化智能训练方案，基于数据分析科学提升骑行表现和竞技水平',
    articleCount: 45,
    icon: 'cpu',
    color: 'amber'
  }
])

const expertArticles = ref([
  {
    id: 1,
    title: '公路自行车空气动力学基础原理',
    author: '平台编辑团队',
    authorTitle: '技术研究组',
    readTime: '15 分钟深度阅读',
    category: '技术深度',
    publishDate: '2024-01-15',
    excerpt: '深入探讨空气阻力对骑行性能的影响，以及如何通过科学的方法优化骑行姿态和装备选择...',
    tags: ['空气动力学', '性能优化', '科学研究']
  },
  {
    id: 2,
    title: '碳纤维车架材料特性分析',
    author: '技术分析师',
    authorTitle: '材料研究专员',
    readTime: '12 分钟深度阅读',
    category: '材料科学',
    publishDate: '2024-01-12',
    excerpt: '从材料科学角度解析碳纤维的分子结构特性，以及不同编织方式对车架性能的影响...',
    tags: ['碳纤维', '材料科学', '车架技术']
  },
  {
    id: 3,
    title: '功率训练数据分析与应用',
    author: '训练数据团队',
    authorTitle: '运动科学研究员',
    readTime: '18 分钟深度阅读',
    category: '训练科学',
    publishDate: '2024-01-10',
    excerpt: '通过数据分析功率训练中的关键指标，为骑行者提供科学的训练指导和性能提升建议...',
    tags: ['功率训练', '数据分析', '训练科学']
  }
])

const searchQuery = ref('')
const isSearchFocused = ref(false)

// 获取图标组件
const getIconComponent = (iconName: string) => {
  const icons = {
    book: `<path d="M4 19.5A2.5 2.5 0 0 1 6.5 17H20"/><path d="M6.5 2H20v20H6.5A2.5 2.5 0 0 1 4 19.5v-15A2.5 2.5 0 0 1 6.5 2z"/>`,
    activity: `<polyline points="22,12 18,12 15,21 9,3 6,12 2,12"/>`,
    settings: `<circle cx="12" cy="12" r="3"/><path d="M12 1v6m0 6v6m11-7h-6m-6 0H1m17-4a4 4 0 0 1-8 0 4 4 0 0 1 8 0zM7 21a4 4 0 0 1-8 0 4 4 0 0 1 8 0z"/>`,
    cpu: `<rect x="4" y="4" width="16" height="16" rx="2"/><rect x="9" y="9" width="6" height="6"/><path d="M9 1v3M15 1v3M9 20v3M15 20v3M20 9h3M20 15h3M1 9h3M1 15h3"/>`
  }
  return icons[iconName as keyof typeof icons] || icons.book
}
</script>

<template>
  <div class="home-page">
    <!-- 主视觉区域 - 重新设计 -->
    <section class="home-page__hero">
      <div class="home-page__hero-container">
        <div class="home-page__hero-content">
          <h1 class="home-page__hero-title">{{ heroContent.title }}</h1>
          <p class="home-page__hero-subtitle">{{ heroContent.subtitle }}</p>
          <p class="home-page__hero-description">{{ heroContent.description }}</p>
          
          <!-- 优化后的搜索框 - 更加融合 -->
          <div class="home-page__search-container">
            <div class="home-page__search-box" :class="{ 'home-page__search-box--focused': isSearchFocused }">
              <svg class="home-page__search-icon" viewBox="0 0 24 24" fill="none" stroke="currentColor">
                <circle cx="11" cy="11" r="8"></circle>
                <path d="m21 21-4.35-4.35"></path>
              </svg>
              <input 
                v-model="searchQuery"
                @focus="isSearchFocused = true"
                @blur="isSearchFocused = false"
                type="text" 
                placeholder="搜索骑行知识、训练方法、装备指南..."
                class="home-page__search-input"
              >
              <div class="home-page__search-actions">
                <button class="home-page__search-submit" type="button">
                  <span>搜索</span>
                </button>
              </div>
            </div>
            <div class="home-page__search-suggestions">
              <span class="home-page__suggestion-tag">功率训练</span>
              <span class="home-page__suggestion-tag">车架选择</span>
              <span class="home-page__suggestion-tag">骑行姿态</span>
              <span class="home-page__suggestion-tag">营养补给</span>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- 知识分类 - 全面优化设计 -->
    <section class="home-page__categories">
      <div class="home-page__section-container">
        <div class="home-page__section-header">
          <h2 class="home-page__section-title">知识体系</h2>
          <p class="home-page__section-subtitle">系统化的专业知识分类，构建完整的公路自行车学习路径</p>
        </div>
        
        <div class="home-page__categories-grid">
          <div 
            v-for="category in featuredCategories" 
            :key="category.id"
            class="home-page__category-card"
            :class="`home-page__category-card--${category.color}`"
          >
            <!-- 卡片装饰元素 -->
            <div class="home-page__category-decoration">
              <div class="home-page__category-decoration-dot"></div>
              <div class="home-page__category-decoration-line"></div>
            </div>
            
            <div class="home-page__category-header">
              <div class="home-page__category-icon-wrapper">
                <svg class="home-page__category-icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" v-html="getIconComponent(category.icon)">
                </svg>
              </div>
              <div class="home-page__category-meta">
                <div class="home-page__category-count">{{ category.articleCount }}</div>
                <div class="home-page__category-count-label">篇文章</div>
              </div>
            </div>
            
            <div class="home-page__category-content">
              <h3 class="home-page__category-title">{{ category.title }}</h3>
              <p class="home-page__category-subtitle">{{ category.subtitle }}</p>
              <p class="home-page__category-description">{{ category.description }}</p>
            </div>
            
            <div class="home-page__category-footer">
              <button class="home-page__category-explore">
                <span>开始学习</span>
                <svg class="home-page__category-arrow" viewBox="0 0 24 24" fill="none" stroke="currentColor">
                  <path d="M5 12h14M12 5l7 7-7 7"/>
                </svg>
              </button>
            </div>
            
            <!-- 悬停效果背景 -->
            <div class="home-page__category-hover-bg"></div>
          </div>
        </div>
      </div>
    </section>

    <!-- 专业内容 -->
    <section class="home-page__articles">
      <div class="home-page__section-container">
        <div class="home-page__section-header">
          <h2 class="home-page__section-title">专业内容</h2>
          <p class="home-page__section-subtitle">基于科学研究的深度分析与专业指导</p>
        </div>
        
        <div class="home-page__articles-grid">
          <article 
            v-for="article in expertArticles" 
            :key="article.id"
            class="home-page__article-card"
          >
            <div class="home-page__article-header">
              <span class="home-page__article-category">{{ article.category }}</span>
              <span class="home-page__article-date">{{ article.publishDate }}</span>
            </div>
            
            <div class="home-page__article-content">
              <h3 class="home-page__article-title">{{ article.title }}</h3>
              <p class="home-page__article-excerpt">{{ article.excerpt }}</p>
              
              <div class="home-page__article-tags">
                <span 
                  v-for="tag in article.tags" 
                  :key="tag"
                  class="home-page__article-tag"
                >
                  {{ tag }}
                </span>
              </div>
            </div>
            
            <div class="home-page__article-footer">
              <div class="home-page__author-info">
                <div class="home-page__author-avatar">
                  <svg viewBox="0 0 24 24" fill="none" stroke="currentColor">
                    <path d="M20 21v-2a4 4 0 0 0-4-4H8a4 4 0 0 0-4 4v2"/>
                    <circle cx="12" cy="7" r="4"/>
                  </svg>
                </div>
                <div class="home-page__author-details">
                  <div class="home-page__author-name">{{ article.author }}</div>
                  <div class="home-page__author-title">{{ article.authorTitle }}</div>
                </div>
              </div>
              <div class="home-page__article-meta">
                <span class="home-page__read-time">{{ article.readTime }}</span>
                <button class="home-page__read-more">阅读全文</button>
              </div>
            </div>
          </article>
        </div>
      </div>
    </section>

    <!-- 平台数据 -->
    <section class="home-page__stats">
      <div class="home-page__section-container">
        <div class="home-page__stats-grid">
          <div class="home-page__stat-item">
            <div class="home-page__stat-number">500+</div>
            <div class="home-page__stat-label">专业文章</div>
          </div>
          <div class="home-page__stat-item">
            <div class="home-page__stat-number">15</div>
            <div class="home-page__stat-label">知识分类</div>
          </div>
          <div class="home-page__stat-item">
            <div class="home-page__stat-number">AI</div>
            <div class="home-page__stat-label">智能训练</div>
          </div>
          <div class="home-page__stat-item">
            <div class="home-page__stat-number">24/7</div>
            <div class="home-page__stat-label">持续更新</div>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>
