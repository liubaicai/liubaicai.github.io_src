<template>
  <!-- 社交链接 -->
  <div class="social">
    <div class="link">
      <a
        v-for="item in socialLinks"
        :key="item.name"
        :href="item.url"
        target="_blank"
        @mouseenter="socialTip = item.tip"
        @mouseleave="socialTip = '通过这里联系我吧'"
      >
        <img class="icon" :src="item.icon" height="24" />
      </a>
    </div>
    <span class="tip">{{ socialTip }}</span>
  </div>
</template>

<script setup>
import socialLinks from "@/assets/socialLinks.json";

// 社交链接提示
const socialTip = ref("通过这里联系我吧");
</script>

<style lang="scss" scoped>
.social {
  margin-top: 1rem;
  display: flex;
  align-items: center;
  justify-content: space-between;
  max-width: 460px;
  width: 100%;
  height: 42px;
  background-color: transparent;
  border-radius: 6px;
  backdrop-filter: blur(0);
  animation: fade 0.5s;
  transition:
    background-color 0.3s,
    backdrop-filter 0.3s,
    border 0.3s,
    box-shadow 0.3s;
  border: 1px solid transparent;
  
  @media (max-width: 840px) {
    max-width: 100%;
    justify-content: center;
    .link {
      justify-content: space-evenly !important;
      width: 90%;
    }
    .tip {
      display: none !important;
    }
  }

  .link {
    display: flex;
    align-items: center;
    justify-content: center;
    a {
      display: inherit;
      position: relative;
      
      &::before {
        content: '';
        position: absolute;
        inset: -2px;
        border-radius: 50%;
        padding: 2px;
        background: linear-gradient(45deg, transparent, #00ff41, transparent);
        -webkit-mask: linear-gradient(#fff 0 0) content-box, linear-gradient(#fff 0 0);
        -webkit-mask-composite: xor;
        mask: linear-gradient(#fff 0 0) content-box, linear-gradient(#fff 0 0);
        mask-composite: exclude;
        opacity: 0;
        transition: opacity 0.3s;
      }
      
      &:hover::before {
        opacity: 1;
      }
      
      .icon {
        margin: 0 12px;
        transition: transform 0.3s, filter 0.3s;
        filter: drop-shadow(0 0 2px rgba(255, 255, 255, 0.3));
        
        &:hover {
          transform: scale(1.15);
          filter: drop-shadow(0 0 8px rgba(0, 255, 65, 0.8));
        }
        &:active {
          transform: scale(1);
        }
      }
    }
  }
  .tip {
    display: none;
    margin-right: 12px;
    animation: fade 0.5s;
    font-family: "Courier New", "Consolas", monospace;
    color: #00ff41;
    text-shadow: 0 0 5px rgba(0, 255, 65, 0.3);
  }
  @media (min-width: 768px) {
    &:hover {
      background-color: rgba(10, 14, 39, 0.6);
      backdrop-filter: blur(5px);
      border: 1px solid rgba(0, 255, 65, 0.2);
      box-shadow: 0 0 15px rgba(0, 255, 65, 0.1);
      .tip {
        display: block;
      }
    }
  }
}
</style>
