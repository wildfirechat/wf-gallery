<template>
    <div id="app">
        <Gallery />
    </div>
</template>

<script>
import Gallery from './components/Gallery.vue'

export default {
    name: 'App',
    components: {
        Gallery
    }
}
</script>

<style>
/* 全局重置 */
*, *::before, *::after {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

html {
    scroll-behavior: smooth;
}

body {
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', 'PingFang SC', 'Hiragino Sans GB', 'Microsoft YaHei', 'Helvetica Neue', sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    color: #334155;
    line-height: 1.6;
    overflow-x: hidden;
}

#app {
    min-height: 100vh;
}

/* 选中文字颜色 */
::selection {
    background: rgba(102, 126, 234, 0.3);
    color: inherit;
}

/* 滚动条美化 */
::-webkit-scrollbar {
    width: 8px;
    height: 8px;
}

::-webkit-scrollbar-track {
    background: #f1f5f9;
}

::-webkit-scrollbar-thumb {
    background: #cbd5e1;
    border-radius: 4px;
}

::-webkit-scrollbar-thumb:hover {
    background: #94a3b8;
}

/* LightGallery 全局自定义 */
.lg-backdrop {
    background: rgba(15, 23, 42, 0.95) !important;
}

.lg-toolbar {
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%) !important;
}

.lg-toolbar .lg-icon {
    color: white !important;
}

.lg-outer .lg-thumb-outer {
    background: rgba(15, 23, 42, 0.9) !important;
}

.lg-outer .lg-thumb-item {
    border: 2px solid transparent !important;
    border-radius: 4px;
    opacity: 0.6;
    transition: all 0.3s ease;
}

.lg-outer .lg-thumb-item.active,
.lg-outer .lg-thumb-item:hover {
    border-color: #667eea !important;
    opacity: 1;
}

.lg-outer .lg-img-wrap {
    padding: 20px;
}

.lg-outer .lg-image {
    border-radius: 8px;
    box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.5);
}

/* 图片加载占位 */
img {
    background: linear-gradient(90deg, #f0f0f0 25%, #e0e0e0 50%, #f0f0f0 75%);
    background-size: 200% 100%;
    animation: loading 1.5s infinite;
}

img[src] {
    animation: none;
    background: transparent;
}

@keyframes loading {
    0% { background-position: 200% 0; }
    100% { background-position: -200% 0; }
}
</style>
