<template>
  <div id="loader-wrapper" :class="store.imgLoadStatus ? 'loaded' : null">
    <div class="loader">
      <div class="loader-circle" />
      <div class="loader-text">
        <span class="name">
          {{ siteName }}
        </span>
        <span class="tip"> 加载中 </span>
      </div>
    </div>
    <div class="loader-section section-left" />
    <div class="loader-section section-right" />
  </div>
</template>

<script setup>
import { mainStore } from "@/store";

const store = mainStore();

// 配置
const siteName = import.meta.env.VITE_SITE_NAME;
</script>

<style lang="scss" scoped>
#loader-wrapper {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 999;
  overflow: hidden;
  .loader {
    width: 100%;
    height: 100%;
    position: absolute;
    top: 0;
    left: 0;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    .loader-circle {
      width: 150px;
      height: 150px;
      border-radius: 50%;
      border: 3px solid transparent;
      border-top-color: #00ff41;
      box-shadow: 0 0 20px rgba(0, 255, 65, 0.5);
      animation: spin 1.8s linear infinite;
      z-index: 2;

      &:before {
        content: "";
        position: absolute;
        top: 5px;
        left: 5px;
        right: 5px;
        bottom: 5px;
        border-radius: 50%;
        border: 3px solid transparent;
        border-top-color: rgba(0, 255, 65, 0.6);
        animation: spin-reverse 0.6s linear infinite;
      }

      &:after {
        content: "";
        position: absolute;
        top: 15px;
        left: 15px;
        right: 15px;
        bottom: 15px;
        border-radius: 50%;
        border: 3px solid transparent;
        border-top-color: rgba(0, 255, 65, 0.4);
        animation: spin 1s linear infinite;
      }
    }
    .loader-text {
      display: flex;
      flex-direction: column;
      align-items: center;
      color: #00ff41;
      z-index: 2;
      margin-top: 40px;
      font-size: 24px;
      font-family: "Courier New", "Consolas", monospace;
      text-shadow: 0 0 10px rgba(0, 255, 65, 0.5);
      
      .name {
        animation: text-glow 2s ease-in-out infinite;
      }
      
      .tip {
        margin-top: 6px;
        font-size: 18px;
        opacity: 0.8;
        
        &::after {
          content: '...';
          animation: loading-dots 1.5s steps(4) infinite;
        }
      }
    }
  }
  .loader-section {
    position: fixed;
    top: 0;
    width: 51%;
    height: 100%;
    background: #0a0e27;
    z-index: 1;
    border: 1px solid rgba(0, 255, 65, 0.2);
    box-shadow: 0 0 30px rgba(0, 255, 65, 0.1);
    
    &.section-left {
      left: 0;
      border-right: 2px solid rgba(0, 255, 65, 0.3);
    }
    &.section-right {
      right: 0;
      border-left: 2px solid rgba(0, 255, 65, 0.3);
    }
  }
  &.loaded {
    visibility: hidden;
    transform: translateY(-100%);
    transition:
      transform 0.3s 1s ease-out,
      visibility 0.3s 1s ease-out;
    .loader {
      .loader-circle,
      .loader-text {
        opacity: 0;
        transition: opacity 0.3s ease-out;
      }
    }
    .loader-section {
      &.section-left {
        transform: translateX(-100%);
        transition: transform 0.5s 0.3s cubic-bezier(0.645, 0.045, 0.355, 1);
      }
      &.section-right {
        transform: translateX(100%);
        transition: transform 0.5s 0.3s cubic-bezier(0.645, 0.045, 0.355, 1);
      }
    }
  }
}

@keyframes spin {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}

@keyframes spin-reverse {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(-360deg);
  }
}

@keyframes loading-dots {
  0% {
    content: '';
  }
  25% {
    content: '.';
  }
  50% {
    content: '..';
  }
  75%, 100% {
    content: '...';
  }
}
</style>
