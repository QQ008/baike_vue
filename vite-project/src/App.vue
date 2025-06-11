<script setup lang="ts">
import { ref } from 'vue'

// 导航状态
const isMobileMenuOpen = ref(false)
const isSearchOpen = ref(false)
</script>

<template>
  <div id="app">
    <!-- 全局顶部导航栏 - 重新设计 -->
    <header class="app-header">
      <nav class="app-nav">
        <div class="app-nav__container">
          <router-link to="/" class="app-nav__brand">
            <div class="app-nav__brand-icon">
              <svg viewBox="0 0 24 24" fill="none" stroke="currentColor">
                <circle cx="12" cy="12" r="10"/>
                <path d="M12 6v6l4 2"/>
              </svg>
            </div>
            <div class="app-nav__brand-text">
              <h1 class="app-nav__brand-title">CyclopediaPro</h1>
              <p class="app-nav__brand-subtitle">骑行百科与训练平台</p>
            </div>
          </router-link>
          
          <div class="app-nav__menu" :class="{ 'app-nav__menu--open': isMobileMenuOpen }">
            <router-link to="/" class="app-nav__item">
              <span class="app-nav__item-text">首页</span>
            </router-link>
            <router-link to="/knowledge" class="app-nav__item">
              <span class="app-nav__item-text">知识体系</span>
            </router-link>
            <router-link to="/training" class="app-nav__item">
              <span class="app-nav__item-text">AI训练</span>
            </router-link>
            <router-link to="/community" class="app-nav__item">
              <span class="app-nav__item-text">社区</span>
            </router-link>
            <router-link to="/about" class="app-nav__item">
              <span class="app-nav__item-text">关于</span>
            </router-link>
          </div>
          
          <div class="app-nav__actions">
            <button 
              class="app-nav__search-trigger"
              @click="isSearchOpen = !isSearchOpen"
              aria-label="搜索"
            >
              <svg viewBox="0 0 24 24" fill="none" stroke="currentColor">
                <circle cx="11" cy="11" r="8"></circle>
                <path d="m21 21-4.35-4.35"></path>
              </svg>
            </button>
            <button class="app-nav__user-menu" aria-label="用户菜单">
              <svg viewBox="0 0 24 24" fill="none" stroke="currentColor">
                <path d="M20 21v-2a4 4 0 0 0-4-4H8a4 4 0 0 0-4 4v2"/>
                <circle cx="12" cy="7" r="4"/>
              </svg>
            </button>
            <button 
              class="app-nav__mobile-toggle"
              @click="isMobileMenuOpen = !isMobileMenuOpen"
              aria-label="菜单"
            >
              <span></span>
              <span></span>
              <span></span>
            </button>
          </div>
        </div>
        
        <!-- 全局搜索栏 -->
        <div class="app-nav__search" :class="{ 'app-nav__search--open': isSearchOpen }">
          <div class="app-nav__search-container">
            <input 
              type="text" 
              placeholder="搜索知识、训练计划、装备指南..."
              class="app-nav__search-input"
            >
            <button class="app-nav__search-close" @click="isSearchOpen = false">
              <svg viewBox="0 0 24 24" fill="none" stroke="currentColor">
                <line x1="18" y1="6" x2="6" y2="18"></line>
                <line x1="6" y1="6" x2="18" y2="18"></line>
              </svg>
            </button>
          </div>
        </div>
      </nav>
    </header>

    <!-- 主要内容区域 -->
    <main class="app-main">
      <router-view />
    </main>

    <!-- 全局底部 -->
    <footer class="app-footer">
      <div class="app-footer__container">
        <div class="app-footer__brand">
          <h3 class="app-footer__brand-title">CyclopediaPro</h3>
          <p class="app-footer__brand-description">专业公路自行车百科与训练平台</p>
        </div>
        
        <div class="app-footer__links">
          <div class="app-footer__link-group">
            <h4 class="app-footer__link-title">知识中心</h4>
            <router-link to="/basics" class="app-footer__link">基础理论</router-link>
            <router-link to="/equipment" class="app-footer__link">装备科学</router-link>
            <router-link to="/training" class="app-footer__link">训练方法</router-link>
          </div>
          <div class="app-footer__link-group">
            <h4 class="app-footer__link-title">平台服务</h4>
            <router-link to="/ai-training" class="app-footer__link">AI训练计划</router-link>
            <router-link to="/community" class="app-footer__link">骑行社区</router-link>
            <router-link to="/support" class="app-footer__link">技术支持</router-link>
          </div>
          <div class="app-footer__link-group">
            <h4 class="app-footer__link-title">关于我们</h4>
            <router-link to="/team" class="app-footer__link">团队介绍</router-link>
            <router-link to="/mission" class="app-footer__link">平台使命</router-link>
            <router-link to="/contact" class="app-footer__link">联系我们</router-link>
          </div>
        </div>
      </div>
      
      <div class="app-footer__bottom">
        <p class="app-footer__copyright">&copy; 2024 CyclopediaPro. 致力于推动公路自行车运动的科学发展</p>
      </div>
    </footer>
  </div>
</template>

<style>
/* 导入Home页面样式 */
@import './assets/style/home.css';

/* App根组件样式 */
#app {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
}

/* 优化后的全局导航栏 */
.app-header {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  z-index: 1000;
  background: rgba(255, 255, 255, 0.98);
  backdrop-filter: blur(24px);
  border-bottom: 1px solid var(--color-border-primary);
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.05);
}

.app-nav__container {
  max-width: 1400px;
  margin: 0 auto;
  padding: 0 32px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  height: 72px;
}

.app-nav__brand {
  display: flex;
  align-items: center;
  gap: 12px;
  text-decoration: none;
  transition: all 0.3s var(--ease-out-cubic);
}

.app-nav__brand:hover {
  transform: translateY(-1px);
}

.app-nav__brand-icon {
  width: 36px;
  height: 36px;
  background: var(--gradient-primary);
  border-radius: var(--radius-lg);
  display: flex;
  align-items: center;
  justify-content: center;
  color: white;
}

.app-nav__brand-icon svg {
  width: 20px;
  height: 20px;
  stroke-width: 2.5;
}

.app-nav__brand-text {
  line-height: 1.2;
}

.app-nav__brand-title {
  font-size: 20px;
  font-weight: 700;
  color: var(--color-text-primary);
  margin: 0;
  letter-spacing: -0.025em;
}

.app-nav__brand-subtitle {
  font-size: 11px;
  color: var(--color-text-tertiary);
  margin: 0;
  font-weight: 500;
  letter-spacing: 0.05em;
}

.app-nav__menu {
  display: flex;
  gap: 32px;
}

.app-nav__item {
  color: var(--color-text-secondary);
  text-decoration: none;
  font-weight: 500;
  font-size: 15px;
  transition: all 0.3s var(--ease-out-cubic);
  position: relative;
  padding: 12px 0;
  display: flex;
  align-items: center;
}

.app-nav__item:hover {
  color: var(--color-text-primary);
}

.app-nav__item.router-link-active {
  color: var(--color-primary);
}

.app-nav__item::after {
  content: '';
  position: absolute;
  bottom: 0;
  left: 0;
  width: 0;
  height: 2px;
  background: var(--gradient-primary);
  transition: width 0.3s var(--ease-out-cubic);
  border-radius: 1px;
}

.app-nav__item:hover::after,
.app-nav__item.router-link-active::after {
  width: 100%;
}

.app-nav__actions {
  display: flex;
  gap: 12px;
  align-items: center;
}

.app-nav__search-trigger,
.app-nav__user-menu {
  width: 40px;
  height: 40px;
  border: none;
  background: var(--color-bg-secondary);
  border-radius: var(--radius-lg);
  cursor: pointer;
  transition: all 0.3s var(--ease-out-cubic);
  display: flex;
  align-items: center;
  justify-content: center;
  color: var(--color-text-secondary);
}

.app-nav__search-trigger svg,
.app-nav__user-menu svg {
  width: 18px;
  height: 18px;
  stroke-width: 2;
}

.app-nav__search-trigger:hover,
.app-nav__user-menu:hover {
  background: var(--color-bg-tertiary);
  color: var(--color-text-primary);
  transform: translateY(-1px);
}

.app-nav__mobile-toggle {
  display: none;
  flex-direction: column;
  gap: 4px;
  background: none;
  border: none;
  cursor: pointer;
  padding: 8px;
}

.app-nav__mobile-toggle span {
  width: 20px;
  height: 2px;
  background: var(--color-text-primary);
  transition: all 0.3s var(--ease-out-cubic);
  border-radius: 1px;
}

/* 全局搜索栏 */
.app-nav__search {
  position: absolute;
  top: 100%;
  left: 0;
  right: 0;
  background: var(--color-bg-primary);
  border-bottom: 1px solid var(--color-border-primary);
  transform: translateY(-100%);
  opacity: 0;
  visibility: hidden;
  transition: all 0.3s var(--ease-out-cubic);
}

.app-nav__search--open {
  transform: translateY(0);
  opacity: 1;
  visibility: visible;
}

.app-nav__search-container {
  max-width: 1400px;
  margin: 0 auto;
  padding: 24px 32px;
  display: flex;
  align-items: center;
  gap: 16px;
}

.app-nav__search-input {
  flex: 1;
  border: 1px solid var(--color-border-primary);
  border-radius: var(--radius-lg);
  padding: 16px 20px;
  font-size: 16px;
  background: var(--color-bg-secondary);
  transition: all 0.3s var(--ease-out-cubic);
}

.app-nav__search-input:focus {
  outline: none;
  border-color: var(--color-primary);
  box-shadow: 0 0 0 3px rgba(59, 130, 246, 0.1);
}

.app-nav__search-close {
  width: 40px;
  height: 40px;
  border: none;
  background: var(--color-bg-secondary);
  border-radius: var(--radius-lg);
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  color: var(--color-text-secondary);
  transition: all 0.3s var(--ease-out-cubic);
}

.app-nav__search-close svg {
  width: 18px;
  height: 18px;
  stroke-width: 2;
}

.app-nav__search-close:hover {
  background: var(--color-bg-tertiary);
  color: var(--color-text-primary);
}

/* 主要内容区域 */
.app-main {
  flex: 1;
  padding-top: 72px;
}

/* 全局底部 */
.app-footer {
  background: var(--color-bg-secondary);
  border-top: 1px solid var(--color-border-primary);
  margin-top: auto;
}

.app-footer__container {
  max-width: 1400px;
  margin: 0 auto;
  padding: 60px 32px 40px;
  display: grid;
  grid-template-columns: 1fr 2fr;
  gap: 60px;
}

.app-footer__brand-title {
  font-size: 24px;
  font-weight: 700;
  color: var(--color-text-primary);
  margin: 0 0 12px;
}

.app-footer__brand-description {
  color: var(--color-text-secondary);
  margin: 0;
  line-height: 1.6;
}

.app-footer__links {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 40px;
}

.app-footer__link-title {
  font-size: 16px;
  font-weight: 600;
  color: var(--color-text-primary);
  margin: 0 0 16px;
}

.app-footer__link {
  display: block;
  color: var(--color-text-secondary);
  text-decoration: none;
  margin-bottom: 8px;
  transition: color 0.3s var(--ease-out-cubic);
}

.app-footer__link:hover {
  color: var(--color-primary);
}

.app-footer__bottom {
  border-top: 1px solid var(--color-border-primary);
  padding: 24px 32px;
  text-align: center;
}

.app-footer__copyright {
  color: var(--color-text-tertiary);
  margin: 0;
  font-size: 14px;
}

/* 响应式设计 */
@media (max-width: 768px) {
  .app-nav__container {
    padding: 0 20px;
    height: 64px;
  }
  
  .app-nav__menu {
    position: fixed;
    top: 64px;
    left: 0;
    right: 0;
    background: var(--color-bg-primary);
    border-bottom: 1px solid var(--color-border-primary);
    flex-direction: column;
    padding: 20px;
    gap: 20px;
    transform: translateY(-100%);
    opacity: 0;
    visibility: hidden;
    transition: all 0.3s var(--ease-out-cubic);
  }
  
  .app-nav__menu--open {
    transform: translateY(0);
    opacity: 1;
    visibility: visible;
  }
  
  .app-nav__mobile-toggle {
    display: flex;
  }
  
  .app-main {
    padding-top: 64px;
  }
  
  .app-footer__container {
    grid-template-columns: 1fr;
    gap: 40px;
    padding: 40px 20px 30px;
  }
  
  .app-footer__links {
    grid-template-columns: 1fr;
    gap: 30px;
  }
  
  .app-footer__bottom {
    padding: 20px;
  }
  
  .app-nav__search-container {
    padding: 20px;
  }
}
</style>