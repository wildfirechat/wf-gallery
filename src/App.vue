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
    background: rgba(63, 100, 228, 0.3);
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
    background: #3F64E4;
}

/* LightGallery 全局自定义 */
.lg-backdrop {
    background: rgba(15, 23, 42, 0.95) !important;
}

.lg-toolbar {
    background: #3F64E4 !important;
}

.lg-toolbar .lg-icon {
    color: white !important;
}

.lg-outer .lg-thumb-outer {
    background: rgba(15, 23, 42, 0.9) !important;
}

.lg-outer .lg-thumb-item {
    border: 2px solid transparent !important;
    border-radius: 6px;
    opacity: 0.5;
    transition: all 0.3s ease;
    overflow: hidden;
}

.lg-outer .lg-thumb-item.active,
.lg-outer .lg-thumb-item:hover {
    border-color: #3F64E4 !important;
    opacity: 1;
    box-shadow: 0 4px 12px rgba(63, 100, 228, 0.3);
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
    background: linear-gradient(90deg, #e2e8f0 25%, #cbd5e1 50%, #e2e8f0 75%);
    background-size: 200% 100%;
    animation: shimmer 1.5s ease-in-out infinite;
}

img[src] {
    animation: none;
    background: transparent;
}

@keyframes shimmer {
    0% { background-position: 200% 0; }
    100% { background-position: -200% 0; }
}

/* 图片加载完成淡入效果 */
img[src] {
    opacity: 0;
    animation: fadeInImage 0.5s ease forwards;
}

@keyframes fadeInImage {
    to {
        opacity: 1;
    }
}
</style>
