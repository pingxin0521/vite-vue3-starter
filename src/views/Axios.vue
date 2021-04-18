<template>
  <div class="axios-container page-container">
    <div class="page-title">Axios Test Page</div>
    <div class="user-info-container">
      <el-card class="box-card">
        <template #header>
          <div class="card-header">
            <span>PingXin</span>
            <el-button class="button" type="text" @click="getUserInfo"
              >点击获取PingXin信息
            </el-button>
          </div>
        </template>
        <div v-loading="loading" class="info-list-box">
          <div v-if="userInfo?.name" class="text item">name: {{ userInfo?.name }}</div>
          <div v-if="userInfo?.bio" class="text item">bio: {{ userInfo?.bio }}</div>
          <div v-if="userInfo?.blog" class="text item">blog: {{ userInfo?.blog }}</div>
        </div>
      </el-card>
    </div>
  </div>
</template>
<script lang="ts">
  import { defineComponent, ref, Ref } from 'vue';
  import axios from '../utils/axios';

  export default defineComponent({
    name: 'Axios',
    setup() {
      const userInfo: Ref = ref(null);
      const loading = ref(false);
      const getUserInfo = () => {
        loading.value = true;
        axios
          .get('/users/pingxin0521')
          .then((response) => {
            console.log('response: ', response.data);
            userInfo.value = response.data;
            loading.value = false;
          })
          .catch((error) => {
            loading.value = false;
            console.error(error);
          });
      };
      return {
        userInfo,
        loading,
        getUserInfo,
      };
    },
  });
</script>
<style scoped lang="stylus">
  .axios-container {
    .user-info-container {
      display flex
      justify-content center
      width 100%
      .info-list-box {
        padding 10px
        .text {
          font-size: 14px;
        }

        .item {
          margin-bottom: 18px;
        }
      }

      .card-header {
        display: flex;
        justify-content: space-between;
        align-items: center;
      }

      .box-card {
        width: 480px;
      }
    }
  }
</style>
