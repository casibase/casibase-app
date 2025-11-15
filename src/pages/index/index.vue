<template>
  <view class="container">
    <!-- Loading indicator -->
    <view v-if="loading" class="loading-container">
      <view class="loading-spinner"></view>
      <text class="loading-text">Loading...</text>
    </view>
    
    <!-- Error message -->
    <view v-if="error" class="error-container">
      <text class="error-icon">⚠️</text>
      <text class="error-text">{{ error }}</text>
      <text class="error-hint">{{ errorHint }}</text>
      <button @click="reload" class="reload-button">Retry</button>
    </view>
    
    <!-- Web-view component for embedding H5 page -->
    <web-view 
      v-if="!error"
      :src="webUrl" 
      @message="handleMessage"
      @error="handleError"
      @load="handleLoad"
    ></web-view>
  </view>
</template>

<script>
import config from '@/config.js'

export default {
  data() {
    return {
      webUrl: config.casibaseUrl,
      loading: true,
      error: null,
      errorHint: '',
    }
  },
  onLoad() {
    console.log('Loading Casibase page:', this.webUrl)
  },
  methods: {
    handleMessage(event) {
      // Handle messages from the web-view
      console.log('Message from web-view:', event.detail.data)
    },
    handleError(event) {
      console.error('Web-view error:', event)
      this.loading = false
      this.error = 'Failed to load page'
      
      // Provide helpful error hints based on the platform
      // #ifdef MP-WEIXIN
      this.errorHint = 'Please ensure the domain is configured as Business Domain (业务域名) in WeChat MP Console. See documentation for setup instructions.'
      // #endif
      
      // #ifndef MP-WEIXIN
      this.errorHint = 'Please check your network connection and try again.'
      // #endif
    },
    handleLoad(event) {
      console.log('Web-view loaded successfully')
      this.loading = false
      this.error = null
      this.errorHint = ''
    },
    reload() {
      this.loading = true
      this.error = null
      this.errorHint = ''
      // Force reload by updating the URL
      const url = this.webUrl
      this.webUrl = ''
      this.$nextTick(() => {
        this.webUrl = url
      })
    }
  },
}
</script>

<style scoped>
.container {
  width: 100%;
  height: 100vh;
  position: relative;
}

.loading-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100vh;
  background-color: #ffffff;
}

.loading-spinner {
  width: 40rpx;
  height: 40rpx;
  border: 4rpx solid #f3f3f3;
  border-top: 4rpx solid #3498db;
  border-radius: 50%;
  animation: spin 1s linear infinite;
}

@keyframes spin {
  0% { transform: rotate(0deg); }
  100% { transform: rotate(360deg); }
}

.loading-text {
  margin-top: 20rpx;
  font-size: 28rpx;
  color: #666;
}

.error-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100vh;
  padding: 40rpx;
  background-color: #ffffff;
}

.error-icon {
  font-size: 80rpx;
  margin-bottom: 20rpx;
}

.error-text {
  font-size: 32rpx;
  color: #e74c3c;
  text-align: center;
  margin-bottom: 20rpx;
  font-weight: 600;
  line-height: 1.6;
}

.error-hint {
  font-size: 24rpx;
  color: #666;
  text-align: center;
  margin-bottom: 40rpx;
  line-height: 1.8;
  padding: 0 20rpx;
  max-width: 600rpx;
}

.reload-button {
  padding: 20rpx 60rpx;
  background-color: #3498db;
  color: #ffffff;
  border-radius: 8rpx;
  font-size: 28rpx;
  border: none;
}
</style>
