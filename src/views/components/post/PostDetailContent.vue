
<template>
    <div class="profile-page">
        <section class="section-profile-cover section-shaped my-0">
            <div class="shape shape-style-1 shape-primary shape-skew alpha-4" style="background-image: linear-gradient(120deg, #a1c4fd 0%, #c2e9fb 100%);">
            </div>
        </section>
        <section class="section section-skew">
            <div class="container">
                <card shadow class="card-profile mt--300" no-body>
                    <div class="px-4">
                          <div class="row justify-content-center">
                            <div class="col-lg-3 order-lg-2">
                                <div class="card-profile-image">
                                   
                                        <img v-lazy="'../img/theme/job.jpg'" class="rounded-circle">
                                    
                                </div>
                            </div>
                            <div class="col-lg-4 order-lg-3 text-lg-right align-self-lg-center">
                                <div class="card-profile-actions py-4 mt-lg-0">
                                  
  
                                      
                                </div>
                            </div>
                            <div class="col-lg-4 order-lg-1">
                              
                            </div>
                          </div>
                        <div class="text-center mt-5">
                            <h3> {{ post.title }}
                            </h3>
                        
                        </div>
  
                        <div class="content-detail">
                            <div class="h6 mt-4"><i class="ni business_briefcase-24 mr-2"></i> 작성자 : 김재석(운영자)</div>
                            <div class="h6 mt-4"><i class="ni business_briefcase-24 mr-2"></i> 작성일시 : 2024 - xx - xx</div>
                            
                        </div>
                       
  
  
                        <div class="mt-5 py-5 border-top text-center">
                            <div class="row justify-content-center">
  
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
    data() {
      return {
        post: {},
        id: null,
      };
    },
    async created() {
      this.id = this.$route.params.id;
      console.log('Route param id:', this.id);  // 디버깅: id 값이 제대로 할당되었는지 확인
  
      try {
        const response = await axios.get(`http://localhost:8083/api/post/${this.id}`);
        console.log('API response:', response.data);  // 디버깅: API 호출 결과 확인
        this.post = response.data;
      } catch (error) {
        console.error('게시글을 불러오는 데 실패했습니다:', error);
      }
    }
  };
  </script>
  
  <style>
  .content-detail {
  display: flex;
  justify-content: space-between;
  }
  </style>
  