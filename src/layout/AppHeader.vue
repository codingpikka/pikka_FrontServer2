<template>
  <header class="header-global">
    <base-nav
      transparent
      type=""
      effect="light"
      expand
      class="navbar-main"
    >
      <div class="container">
        <div class="header-wrapper">
          <div class="left-section">
            <router-link slot="brand" class="navbar-brand" to="/">
              <img src="../../public/img/brand/wejob.png" alt="logo" />
            </router-link>

            <div class="nav-links">
              <router-link to="/job" class="nav-link">취업</router-link>
              <router-link to="/certification" class="nav-link">자격증</router-link>
              <router-link to="/post" class="nav-link">게시판</router-link>
            </div>
          </div>

          <div class="nav-right">
            <base-dropdown tag="li" class="nav-item">
              <a
                slot="title"
                href="#"
                class="nav-link dropdown-toggle"
                data-toggle="dropdown"
                role="button"
              >
                <img
                  src="../../public/img/icons/common/heander-icon.svg"
                  alt="header-icon"
                  class="header-icon"
                />
              </a>
              <router-link to="/write" class="dropdown-item">글쓰기</router-link>
              <router-link to="/inquiry" class="dropdown-item">문의하기</router-link>
              <router-link to="/history" class="dropdown-item">마이페이지</router-link>
            </base-dropdown>

            <a href="http://localhost:5173/" title="admin" class="admin-link">
              <div class="admin-image">
                <img src="https://image.fmkorea.com/files/attach/new/20200708/486616/2833571032/2979847802/2143cf95b9a0ffdd7f0ee7ac24930063.jpg" alt="Admin" />
              </div>
            </a>
          </div>
        </div>
      </div>
    </base-nav>
  </header>
</template>

<script>
import BaseNav from "@/components/BaseNav";
import BaseDropdown from "@/components/BaseDropdown";

export default {
  components: {
    BaseNav,
    BaseDropdown,
  },
};
</script>

<style scoped>
.navbar-main {
  background-image: linear-gradient(-225deg, #B7F8DB 0%, #50A7C2 100%);
  box-shadow: 0 3px 6px rgba(0,0,0,0.16), 0 3px 6px rgba(0,0,0,0.23);
  padding: 0.5rem 1rem;
}

.container {
  width: 100%;
  max-width: 1140px;
  padding-right: 15px;
  padding-left: 15px;
  margin-right: auto;
  margin-left: auto;
}

.header-wrapper {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.left-section {
  display: flex;
  align-items: center;
}

.navbar-brand img {
  height: 40px;
  margin-right: 1rem;
}

.nav-links {
  display: flex;
}

.nav-link {
  color: #333;
  padding: 0.5rem 1rem;
  text-decoration: none;
  white-space: nowrap;
}

.nav-right {
  display: flex;
  align-items: center;
  margin-left: auto;
}

.header-icon {
  width: 30px;
  height: 30px;
}

.admin-link {
  margin-left: 1rem;
}

.admin-image {
  width: 50px;
  height: 50px;
  overflow: hidden;
  border-radius: 8px;
}

.admin-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

@media (max-width: 991px) {
  .header-wrapper {
    flex-wrap: wrap;
  }

  .left-section {
    flex-wrap: wrap;
    justify-content: center;
    width: 100%;
  }

  .nav-links {
    margin-top: 1rem;
    justify-content: center;
    width: 100%;
  }

  .nav-right {
    margin: 1rem auto 0;
  }
}
</style>