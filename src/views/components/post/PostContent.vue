<template>
    <div>
        <section class="section section-shaped my-0 overflow-hidden">
            <div class="container pt-lg pb-300">
                <!-- 공지사항 섹션 -->
                <div class="row text-center justify-content-center">
                    <div class="col-lg-10">
                        <br>
                        <badge pill type="primary">공지사항</badge>
                        <br>
                        <h2 class="display-3 text-Gray">최신 공지사항</h2>
                        <p class="lead text-Gray">중요한 공지사항을 확인하세요.</p>
                    </div> 
                </div>

                <div class="row row-grid mt-5">
                    <div v-for="notice in notices" :key="notice.notiId" class="col-lg-4">
                        <icon name="ni ni-settings" size="lg" gradient="white" shadow round color="primary"></icon>
                        <h5 class="text-Gray mt-3">{{ notice.notiTitle }}</h5>
                        <p class="text-Black mt-3">{{ truncateContent(notice.notiContents) }}</p>
                        <router-link :to="{ name: 'UserNoticeDetail', params: { id: notice.notiId } }">
                            <badge tag="a" type="info">상세보기</badge>
                        </router-link>
                    </div>
                </div>

                <!-- 자유게시판 섹션 -->
                <div class="row text-center justify-content-center mt-5">
                    <div class="col-lg-10">
                        <br>
                        <badge pill type="primary">자유게시판</badge>
                        <br>
                        <h2 class="display-3 text-Gray">자유 게시판</h2>
                        <p class="lead text-Gray">
                            여기는 자유롭게 아무거나 사람들이 글을 쓸 수 있는 공간입니다.
                            깔끔하게 정리된 게시물을 볼 수 있는 화면으로 만들어야겠습니다.
                        </p>
                    </div> 
                </div>

                <div class="row row-grid mt-5">
                    <div v-for="i in 3" :key="i" class="col-lg-4">
                        <icon :name="getRandomIcon()" size="lg" gradient="white" shadow round color="primary"></icon>
                        <h5 class="text-Gray mt-3">자유게시판 게시물 제목 {{ i }}</h5>
                        <p class="text-Black mt-3">이것은 자유게시판 게시물의 내용 일부입니다. 내용의 요약본 또는 설명글을 보여줍니다.</p>
                        <router-link to="/postdetail">
                            <badge tag="a" type="info">상세보기</badge>
                        </router-link>
                    </div>
                </div>
            </div>
        </section>
    </div>
</template>

<script>
import axios from 'axios';

export default {
    name: "home",
    data() {
        return {
            notices: []
        };
    },
    created() {
        this.fetchNotices();
    },
    methods: {
        async fetchNotices() {
            try {
                const response = await axios.get('http://localhost:8083/api/notice');
                this.notices = response.data
                    .sort((a, b) => new Date(b.notiCreateAt) - new Date(a.notiCreateAt))
                    .slice(0, 3);
            } catch (error) {
                console.error('공지사항을 불러오는데 실패했습니다:', error);
            }
        },
        truncateContent(content) {
            return content.length > 100 ? content.slice(0, 100) + '...' : content;
        },
        getRandomIcon() {
            const icons = ['ni-settings', 'ni-ruler-pencil', 'ni-atom'];
            return icons[Math.floor(Math.random() * icons.length)];
        }
    }
};
</script>

<style scoped>
.section-shaped {
    padding-top: 5rem;
    padding-bottom: 5rem;
}

.text-Gray {
    color: #333;
}

.text-Black {
    color: #000;
}

.badge {
    cursor: pointer;
}
</style>