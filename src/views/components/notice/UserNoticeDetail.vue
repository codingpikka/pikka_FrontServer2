<template>
  <div class="profile-page">
    <section class="section-profile-cover section-shaped my-0">
      <div class="shape shape-style-1 shape-primary shape-skew alpha-4" style="background-image: linear-gradient(120deg, #a1c4fd 0%, #c2e9fb 100%);">
      </div>
    </section>
    <section class="section section-skew">
      <div class="container">
        <card shadow class="card-profile mt--300" no-body>
          <div class="px-4" v-if="notice">
            <div class="row justify-content-center">
              <div class="col-lg-3 order-lg-2">
                <div class="card-profile-image">
                  <img v-lazy="'img/theme/job.jpg'" class="rounded-circle">
                </div>
              </div>
              <div class="col-lg-4 order-lg-3 text-lg-right align-self-lg-center">
                <div class="card-profile-actions py-4 mt-lg-0">
                  <br> 
                  <br>
                </div>
              </div>
              <div class="col-lg-4 order-lg-1">
              </div>
            </div>
            <div class="text-center mt-5">
              <h3>{{ notice.notiTitle }}</h3>
            </div>

            <div class="content-detail">
              <div class="h6 mt-4"><i class="ni business_briefcase-24 mr-2"></i> 작성자 : {{ notice.notiAdminName }}</div>
              <div class="h6 mt-4"><i class="ni business_briefcase-24 mr-2"></i> 작성일시 : {{ formatDate(notice.notiCreateAt) }}</div>
            </div>

            <div class="mt-5 py-5 border-top text-center">
              <div class="row justify-content-center">
                <div class="col-lg-9">
                  <p>{{ notice.notiContents }}</p>
                </div>
              </div>
              <div>
                <div class="h6 mt-4 text-left"> 댓글 </div>
                <div class="mt-5 py-5 border-top text-center">
                </div>
              </div>

              <div class="col-md-10">
                <base-input placeholder="댓글을 입력하세요(최대300)" addon-right-icon="ni ni-zoom-split-in"></base-input>
              </div>
            </div>
          </div>
        </card>
      </div>
    </section>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'UserNoticeDetail',
  data() {
    return {
      notice: null
    };
  },
  created() {
    this.fetchNotice();
  },
  methods: {
    async fetchNotice() {
      try {
        const id = this.$route.params.id;
        console.log('Fetching notice with id:', id);
        const response = await axios.get(`http://localhost:8083/api/notice/${id}`);
        console.log('API response:', response.data);
        this.notice = response.data;
      } catch (error) {
        console.error('공지사항을 불러오는데 실패했습니다:', error.response || error);
      }
    },
    formatDate(dateString) {
      if (!dateString) return '';
      return new Date(dateString).toLocaleDateString('ko-KR', {
        year: 'numeric',
        month: 'long',
        day: 'numeric',
        hour: '2-digit',
        minute: '2-digit'
      });
    }
  }
};
</script>

<style scoped>
.content-detail {
  display: flex;
  justify-content: space-between;
}
.user-notice-detail {
  max-width: 800px;
  margin: 0 auto;
}
.notice-content {
  white-space: pre-wrap;
}
</style>