<template>
    <div class="gallery-page">
        <!-- 分类导航 -->
        <nav class="nav-bar nav-fixed">
            <div class="nav-scroll">
                <button 
                    v-for="(cat, index) in allCategories" 
                    :key="index"
                    class="nav-item"
                    :class="{ active: currentCategory === cat.id }"
                    @click="scrollToCategory(cat.id)"
                >
                    <span class="nav-icon">{{ cat.icon }}</span>
                    <span class="nav-text">{{ cat.shortName }}</span>
                </button>
            </div>
        </nav>

        <!-- 主内容 -->
        <main class="content" ref="content">
            <!-- 移动端分类 -->
            <div class="category-group">
                <div class="group-header">
                    <span class="group-icon">📱</span>
                    <h2 class="group-title">移动端</h2>
                </div>
                
                <section 
                    v-for="(shot, index) in mobileScreenShots" 
                    :key="'m-' + index"
                    :id="'cat-' + index"
                    class="section"
                >
                    <div class="section-info">
                        <h3 class="section-name">{{ shot.category }}</h3>
                        <span class="section-count">{{ shot.images.length }} 张</span>
                    </div>
                    
                    <div class="mobile-gallery">
                        <div :id="'lightgallery-mobile-' + index" class="mobile-grid">
                            <a 
                                v-for="(url, i) in shot.images" 
                                :href="url" 
                                :key="i"
                                class="mobile-item"
                                :style="{ animationDelay: (i * 50) + 'ms' }"
                            >
                                <div class="phone-frame">
                                    <div class="phone-notch"></div>
                                    <div class="phone-screen">
                                        <img :src="url" :alt="shot.category" loading="lazy" />
                                    </div>
                                </div>
                                <div class="item-overlay">
                                    <svg class="zoom-icon" viewBox="0 0 24 24">
                                        <path d="M15.5 14h-.79l-.28-.27C15.41 12.59 16 11.11 16 9.5 16 5.91 13.09 3 9.5 3S3 5.91 3 9.5 5.91 16 9.5 16c1.61 0 3.09-.59 4.23-1.57l.27.28v.79l5 4.99L20.49 19l-4.99-5zm-6 0C7.01 14 5 11.99 5 9.5S7.01 5 9.5 5 14 7.01 14 9.5 11.99 14 9.5 14z"/>
                                        <path d="M12 10h-2v2H9v-2H7V9h2V7h1v2h2v1z"/>
                                    </svg>
                                </div>
                            </a>
                        </div>
                    </div>
                </section>
            </div>

            <!-- PC端分类 -->
            <div class="category-group">
                <div class="group-header">
                    <span class="group-icon">💻</span>
                    <h2 class="group-title">桌面端</h2>
                </div>
                
                <section 
                    v-for="(shot, index) in pcScreenShots" 
                    :key="'p-' + index"
                    :id="'cat-' + (mobileScreenShots.length + index)"
                    class="section"
                >
                    <div class="section-info">
                        <h3 class="section-name">{{ shot.category }}</h3>
                        <span class="section-count">{{ shot.images.length }} 张</span>
                    </div>
                    
                    <div class="pc-gallery">
                        <div :id="'lightgallery-pc-' + index" class="pc-grid">
                            <a 
                                v-for="(url, i) in shot.images" 
                                :href="url" 
                                :key="i"
                                class="pc-item"
                                :style="{ animationDelay: (i * 80) + 'ms' }"
                            >
                                <div class="monitor-frame">
                                    <div class="monitor-header">
                                        <span class="dot red"></span>
                                        <span class="dot yellow"></span>
                                        <span class="dot green"></span>
                                    </div>
                                    <div class="monitor-screen">
                                        <img :src="url" :alt="shot.category" loading="lazy" />
                                    </div>
                                </div>
                                <div class="item-overlay">
                                    <svg class="zoom-icon" viewBox="0 0 24 24">
                                        <path d="M15.5 14h-.79l-.28-.27C15.41 12.59 16 11.11 16 9.5 16 5.91 13.09 3 9.5 3S3 5.91 3 9.5 5.91 16 9.5 16c1.61 0 3.09-.59 4.23-1.57l.27.28v.79l5 4.99L20.49 19l-4.99-5zm-6 0C7.01 14 5 11.99 5 9.5S7.01 5 9.5 5 14 7.01 14 9.5 11.99 14 9.5 14z"/>
                                        <path d="M12 10h-2v2H9v-2H7V9h2V7h1v2h2v1z"/>
                                    </svg>
                                </div>
                            </a>
                        </div>
                    </div>
                </section>
            </div>
        </main>

        <!-- 返回顶部 -->
        <button 
            class="back-to-top" 
            :class="{ show: showBackToTop }"
            @click="scrollToTop"
        >
            <svg viewBox="0 0 24 24">
                <path d="M7.41 15.41L12 10.83l4.59 4.58L18 14l-6-6-6 6z"/>
            </svg>
        </button>
    </div>
</template>

<script>
import 'lightgallery'
import 'lightgallery/css/lightgallery.css'
import lightGallery from "lightgallery";

export default {
    name: 'Gallery',
    data() {
        return {
            currentCategory: 'cat-0',
            showBackToTop: false,
            mobileScreenShots: [
                {
                    category: "Android",
                    shortName: "Android",
                    icon: "🤖",
                    images: [
                        "https://static.wildfirechat.cn/wf-android-demo-1.jpg",
                        "https://static.wildfirechat.cn/wf-android-demo-2.jpg",
                        "https://static.wildfirechat.cn/wf-android-demo-3.jpg",
                        "https://static.wildfirechat.cn/wf-android-demo-4.jpg",
                        "https://static.wildfirechat.cn/wf-android-demo-5.jpg",
                        "https://static.wildfirechat.cn/wf-android-demo-6.jpg",
                        "https://static.wildfirechat.cn/wf-android-demo-7.jpg",
                        "https://static.wildfirechat.cn/wf-android-demo-8.jpg",
                        "https://static.wildfirechat.cn/wf-android-demo-9.jpg",
                        "https://static.wildfirechat.cn/wf-android-demo-10.jpg",
                        "https://static.wildfirechat.cn/wf-android-demo-11.jpg",
                        "https://static.wildfirechat.cn/wf-android-demo-12.jpg",
                        "https://static.wildfirechat.cn/wf-android-demo-13.jpg",
                        "https://static.wildfirechat.cn/wf-android-demo-14.jpg",
                        "https://static.wildfirechat.cn/wf-android-demo-15.jpg",
                        "https://static.wildfirechat.cn/wf-android-demo-16.jpg",
                        "https://static.wildfirechat.cn/wf-android-demo-17.jpg",
                        "https://static.wildfirechat.cn/wf-android-demo-18.jpg",
                        "https://static.wildfirechat.cn/wf-android-demo-19.jpg",
                    ]
                },
                {
                    category: "iOS",
                    shortName: "iOS",
                    icon: "🍎",
                    images: [
                        "https://static.wildfirechat.cn/ios-message-view.png",
                        "https://static.wildfirechat.cn/ios-contact-view.png",
                        "https://static.wildfirechat.cn/ios-discover-view.png",
                        "https://static.wildfirechat.cn/ios-settings-view.png",
                        "https://static.wildfirechat.cn/ios-messagelist-view.png",
                        "https://static.wildfirechat.cn/ios-chat-setting-view.png",
                        "https://static.wildfirechat.cn/ios-takephoto-view.png",
                        "https://static.wildfirechat.cn/ios-record-voice-view.png",
                        "https://static.wildfirechat.cn/ios-location-view.png",
                        "https://static.wildfirechat.cn/ios-voip-view.png"
                    ]
                },
                {
                    category: "微信小程序",
                    shortName: "小程序",
                    icon: "💬",
                    images: [
                        "https://static.wildfirechat.cn/wx-conversation_list.png",
                        "https://static.wildfirechat.cn/wx-conversation.png",
                        "https://static.wildfirechat.cn/wx-conversation_1.png",
                        "https://static.wildfirechat.cn/wx-friends.png",
                    ]
                },
                {
                    category: "uni-app",
                    shortName: "uni-app",
                    icon: "📱",
                    images: [
                        "https://static.wildfirechat.cn/uniapp_contact_tab.jpeg",
                        "https://static.wildfirechat.cn/uniapp_conversation.jpeg",
                        "https://static.wildfirechat.cn/uniapp_conversation_list.jpeg",
                        "https://static.wildfirechat.cn/uniapp_user_profile.jpeg",
                    ]
                },
            ],
            pcScreenShots: [
                {
                    category: "PC客户端",
                    shortName: "PC",
                    icon: "🖥️",
                    images: [
                        "https://static.wildfirechat.cn/pc-home.png",
                        "https://static.wildfirechat.cn/pc-conversastion.png",
                        "https://static.wildfirechat.cn/pc-emoji.png",
                        "https://static.wildfirechat.cn/pc-contact.png",
                        "https://static.wildfirechat.cn/pc-channel.png",
                        "https://static.wildfirechat.cn/pc-fav.png",
                        "https://static.wildfirechat.cn/pc-file-history.png",
                        "https://static.wildfirechat.cn/pc-workspace.png",
                        "https://static.wildfirechat.cn/pc-setting.png",
                        "https://static.wildfirechat.cn/pc-multi-video-call.png",
                        "https://static.wildfirechat.cn/pc-multi-audio-call.png",
                    ],
                },
                {
                    category: "Web端",
                    shortName: "Web",
                    icon: "🌐",
                    images: [
                        "https://static.wildfirechat.cn/web-home.png",
                        "https://static.wildfirechat.cn/web-conversation.png",
                        "https://static.wildfirechat.cn/web-contact.png",
                        "https://static.wildfirechat.cn/web-channel.png",
                        "https://static.wildfirechat.cn/web-emoji.png",
                        "https://static.wildfirechat.cn/web-forward.png",
                        "https://static.wildfirechat.cn/web-setting.png",
                        "https://static.wildfirechat.cn/web-multi-video-call.png",
                        "https://static.wildfirechat.cn/web-multi-audio-call.png",
                    ],
                },
                {
                    category: "管理后台",
                    shortName: "后台",
                    icon: "⚙️",
                    images: [
                        "https://static.wildfirechat.cn/admin-login.png",
                        "https://static.wildfirechat.cn/admin-home.png",
                        "https://static.wildfirechat.cn/admin-user-list.png",
                        "https://static.wildfirechat.cn/admin-blocked-list.png",
                        "https://static.wildfirechat.cn/admin-sensitive-word-list.png",
                        "https://static.wildfirechat.cn/admin-sensitive-word-match.png",
                        "https://static.wildfirechat.cn/admin-group-list.png",
                        "https://static.wildfirechat.cn/admin-message-list.png",
                        "https://static.wildfirechat.cn/admin-user-message-list.png",
                        "https://static.wildfirechat.cn/admin-broadcast.png",
                        "https://static.wildfirechat.cn/admin-multi-send.png",
                        "https://static.wildfirechat.cn/admin-robot-list.png",
                        "https://static.wildfirechat.cn/admin-channel-list.png",
                    ],
                },
                {
                    category: "开放平台",
                    shortName: "开放平台",
                    icon: "🔌",
                    images: [
                        "https://static.wildfirechat.cn/open-home.png",
                        "https://static.wildfirechat.cn/open-channel.png",
                        "https://static.wildfirechat.cn/open-robot.png",
                        "https://static.wildfirechat.cn/open-robot-create.png",
                    ],
                },
                {
                    category: "频道管理",
                    shortName: "频道",
                    icon: "📢",
                    images: [
                        "https://static.wildfirechat.cn/channel-login.png",
                        "https://static.wildfirechat.cn/channel-channel-menu.png",
                        "https://static.wildfirechat.cn/channel-auto-reply.png",
                        "https://static.wildfirechat.cn/channel-account.png",
                        "https://static.wildfirechat.cn/channel-fans.png",
                        "https://static.wildfirechat.cn/channel-message.png",
                        "https://static.wildfirechat.cn/channel-article.png",
                        "https://static.wildfirechat.cn/channel-media.png",
                    ],
                }
            ],
        }
    },

    computed: {
        allCategories() {
            const categories = [];
            this.mobileScreenShots.forEach((item, index) => {
                categories.push({ 
                    id: 'cat-' + index, 
                    name: item.category,
                    shortName: item.shortName,
                    icon: item.icon
                });
            });
            this.pcScreenShots.forEach((item, index) => {
                categories.push({ 
                    id: 'cat-' + (this.mobileScreenShots.length + index), 
                    name: item.category,
                    shortName: item.shortName,
                    icon: item.icon
                });
            });
            return categories;
        }
    },

    mounted() {
        this.initLightGallery();
        this.handleScroll();
        window.addEventListener('scroll', this.handleScroll, { passive: true });
        
        // URL 参数处理
        setTimeout(() => {
            const params = new URL(location.href).searchParams;
            let t = params.get('t');
            if (t !== null) {
                this.scrollToCategory('cat-' + t);
            }
        }, 300);
    },

    beforeDestroy() {
        window.removeEventListener('scroll', this.handleScroll);
    },

    methods: {
        initLightGallery() {
            this.mobileScreenShots.forEach((_, i) => {
                const el = document.getElementById('lightgallery-mobile-' + i);
                if (el) {
                    lightGallery(el, {
                        selector: 'a',
                        download: false,
                        share: false,
                        thumbnail: true,
                        animateThumb: true,
                        showThumbByDefault: true
                    });
                }
            });
            
            this.pcScreenShots.forEach((_, i) => {
                const el = document.getElementById('lightgallery-pc-' + i);
                if (el) {
                    lightGallery(el, {
                        selector: 'a',
                        download: false,
                        share: false,
                        thumbnail: true,
                        animateThumb: true,
                        showThumbByDefault: true
                    });
                }
            });
        },

        handleScroll() {
            const scrollY = window.scrollY;
            this.showBackToTop = scrollY > 500;

            // 检测当前分类
            const sections = document.querySelectorAll('.section');
            sections.forEach(section => {
                const rect = section.getBoundingClientRect();
                if (rect.top <= 150 && rect.bottom >= 150) {
                    this.currentCategory = section.id;
                }
            });
        },

        scrollToCategory(id) {
            const el = document.getElementById(id);
            if (el) {
                const navHeight = 60;
                const top = el.offsetTop - navHeight - 20;
                window.scrollTo({ top, behavior: 'smooth' });
            }
        },

        scrollToTop() {
            window.scrollTo({ top: 0, behavior: 'smooth' });
        }
    }
}
</script>

<style scoped>
/* 基础样式 */
.gallery-page {
    min-height: 100vh;
    background: #f8fafc;
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', 'PingFang SC', 'Microsoft YaHei', sans-serif;
}

/* 导航栏 - 固定在顶部 */
.nav-bar {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    background: rgba(255, 255, 255, 0.98);
    border-bottom: 1px solid rgba(0, 0, 0, 0.05);
    box-shadow: 0 4px 20px rgba(0, 0, 0, 0.05);
    z-index: 100;
}

.nav-scroll {
    display: flex;
    gap: 8px;
    padding: 12px 20px;
    overflow-x: auto;
    scrollbar-width: none;
    -ms-overflow-style: none;
    max-width: 1200px;
    margin: 0 auto;
}

.nav-scroll::-webkit-scrollbar {
    display: none;
}

.nav-item {
    flex-shrink: 0;
    display: flex;
    align-items: center;
    gap: 6px;
    padding: 10px 18px;
    border: none;
    background: transparent;
    border-radius: 25px;
    font-size: 14px;
    color: #64748b;
    cursor: pointer;
    transition: all 0.3s ease;
    white-space: nowrap;
}

.nav-item:hover {
    background: #f1f5f9;
    color: #334155;
}

.nav-item.active {
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    color: white;
    box-shadow: 0 4px 15px rgba(102, 126, 234, 0.3);
}

.nav-icon {
    font-size: 16px;
}

/* 主内容 */
.content {
    max-width: 1400px;
    margin: 0 auto;
    padding: 100px 20px 40px;
}

/* 分组 */
.category-group {
    margin-bottom: 60px;
}

.group-header {
    display: flex;
    align-items: center;
    gap: 10px;
    margin-bottom: 25px;
    padding-bottom: 12px;
    border-bottom: 2px solid #e2e8f0;
}

.group-icon {
    font-size: 24px;
}

.group-title {
    font-size: 24px;
    font-weight: 700;
    color: #1e293b;
    margin: 0;
}

/* 区块 */
.section {
    margin-bottom: 40px;
}

.section-info {
    display: flex;
    align-items: center;
    justify-content: space-between;
    margin-bottom: 15px;
}

.section-name {
    font-size: 18px;
    font-weight: 600;
    color: #334155;
    margin: 0;
}

.section-count {
    font-size: 12px;
    color: #94a3b8;
    background: #f1f5f9;
    padding: 3px 10px;
    border-radius: 10px;
}

/* 移动端画廊 */
.mobile-gallery {
    overflow-x: auto;
    overflow-y: hidden;
    scrollbar-width: thin;
    scrollbar-color: #cbd5e1 transparent;
    padding: 10px 0 15px;
    margin: 0 -20px;
    padding-left: 20px;
}

.mobile-gallery::-webkit-scrollbar {
    height: 4px;
}

.mobile-gallery::-webkit-scrollbar-track {
    background: transparent;
}

.mobile-gallery::-webkit-scrollbar-thumb {
    background: #cbd5e1;
    border-radius: 2px;
}

.mobile-grid {
    display: flex;
    gap: 15px;
    padding-right: 20px;
}

.mobile-item {
    flex-shrink: 0;
    position: relative;
    text-decoration: none;
    animation: slideIn 0.5s ease-out backwards;
}

@keyframes slideIn {
    from {
        opacity: 0;
        transform: translateX(20px);
    }
    to {
        opacity: 1;
        transform: translateX(0);
    }
}

/* 手机框架 */
.phone-frame {
    width: 140px;
    height: 280px;
    background: #0f0f0f;
    border-radius: 18px;
    padding: 4px;
    box-shadow: 
        0 15px 35px -10px rgba(0, 0, 0, 0.3),
        0 0 0 1px rgba(255, 255, 255, 0.08) inset;
    position: relative;
    transition: transform 0.3s ease;
}

.phone-frame:hover {
    transform: translateY(-3px);
}

.phone-notch {
    position: absolute;
    top: 4px;
    left: 50%;
    transform: translateX(-50%);
    width: 45px;
    height: 14px;
    background: #0f0f0f;
    border-radius: 0 0 8px 8px;
    z-index: 2;
}

.phone-screen {
    width: 100%;
    height: 100%;
    background: #000;
    border-radius: 14px;
    overflow: hidden;
}

.phone-screen img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    transition: transform 0.5s ease;
}

.mobile-item:hover .phone-screen img {
    transform: scale(1.05);
}

/* PC端画廊 */
.pc-gallery {
    overflow-x: auto;
    overflow-y: hidden;
    scrollbar-width: thin;
    scrollbar-color: #cbd5e1 transparent;
    padding: 10px 0 15px;
    margin: 0 -20px;
    padding-left: 20px;
}

.pc-gallery::-webkit-scrollbar {
    height: 4px;
}

.pc-gallery::-webkit-scrollbar-track {
    background: transparent;
}

.pc-gallery::-webkit-scrollbar-thumb {
    background: #cbd5e1;
    border-radius: 2px;
}

.pc-grid {
    display: flex;
    gap: 20px;
    padding-right: 20px;
}

.pc-item {
    flex-shrink: 0;
    position: relative;
    text-decoration: none;
    animation: slideIn 0.5s ease-out backwards;
}

/* 显示器框架 - 无底座 */
.monitor-frame {
    width: 260px;
    background: #1a1a2e;
    border-radius: 8px;
    padding: 3px;
    box-shadow: 0 15px 35px -10px rgba(0, 0, 0, 0.3);
    transition: transform 0.3s ease;
}

.monitor-frame:hover {
    transform: translateY(-3px);
}

.monitor-header {
    height: 20px;
    background: #2d2d44;
    border-radius: 6px 6px 0 0;
    display: flex;
    align-items: center;
    gap: 5px;
    padding: 0 10px;
}

.dot {
    width: 6px;
    height: 6px;
    border-radius: 50%;
}

.dot.red { background: #ff5f56; }
.dot.yellow { background: #ffbd2e; }
.dot.green { background: #27ca40; }

.monitor-screen {
    width: 100%;
    aspect-ratio: 16/10;
    background: #1a1a2e;
    border-radius: 0 0 5px 5px;
    overflow: hidden;
}

.monitor-screen img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    transition: transform 0.5s ease;
}

.pc-item:hover .monitor-screen img {
    transform: scale(1.03);
}

/* 悬停遮罩 */
.item-overlay {
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background: rgba(0, 0, 0, 0.4);
    display: flex;
    align-items: center;
    justify-content: center;
    opacity: 0;
    transition: opacity 0.3s ease;
    border-radius: 18px;
}

.pc-item .item-overlay {
    border-radius: 8px;
}

.mobile-item:hover .item-overlay,
.pc-item:hover .item-overlay {
    opacity: 1;
}

.zoom-icon {
    width: 40px;
    height: 40px;
    fill: white;
    transform: scale(0.5);
    transition: transform 0.3s ease;
}

.mobile-item:hover .zoom-icon,
.pc-item:hover .zoom-icon {
    transform: scale(1);
}

/* 返回顶部 */
.back-to-top {
    position: fixed;
    bottom: 25px;
    right: 25px;
    width: 44px;
    height: 44px;
    border: none;
    border-radius: 50%;
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    color: white;
    cursor: pointer;
    box-shadow: 0 4px 15px rgba(102, 126, 234, 0.4);
    opacity: 0;
    transform: translateY(20px);
    transition: all 0.3s ease;
    z-index: 99;
    display: flex;
    align-items: center;
    justify-content: center;
}

.back-to-top.show {
    opacity: 1;
    transform: translateY(0);
}

.back-to-top:hover {
    transform: translateY(-3px);
    box-shadow: 0 6px 20px rgba(102, 126, 234, 0.5);
}

.back-to-top svg {
    width: 22px;
    height: 22px;
    fill: currentColor;
}

/* 响应式 - 平板 */
@media (max-width: 1024px) {
    .phone-frame {
        width: 130px;
        height: 260px;
    }
    
    .monitor-frame {
        width: 240px;
    }
}

/* 响应式 - 手机 */
@media (max-width: 640px) {
    .content {
        padding-top: 80px;
    }
    
    .nav-item {
        padding: 8px 14px;
        font-size: 13px;
    }
    
    .nav-text {
        display: none;
    }
    
    .group-title {
        font-size: 20px;
    }
    
    .section-name {
        font-size: 16px;
    }
    
    .phone-frame {
        width: 110px;
        height: 220px;
        border-radius: 16px;
    }
    
    .phone-notch {
        width: 40px;
        height: 12px;
        border-radius: 0 0 6px 6px;
    }
    
    .phone-screen {
        border-radius: 12px;
    }
    
    .monitor-frame {
        width: 220px;
    }
    
    .mobile-grid,
    .pc-grid {
        gap: 12px;
    }
    
    .back-to-top {
        width: 40px;
        height: 40px;
        bottom: 15px;
        right: 15px;
    }
}

/* LightGallery 自定义 */
:global(.lg-backdrop) {
    background: rgba(15, 23, 42, 0.95) !important;
}

:global(.lg-toolbar) {
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%) !important;
}

:global(.lg-thumb-outer) {
    background: rgba(15, 23, 42, 0.9) !important;
}

:global(.lg-thumb-item.active) {
    border-color: #667eea !important;
}
</style>
