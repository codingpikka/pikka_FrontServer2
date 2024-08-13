<template>
  <footer class="footer">
    <div class="container">
      <div class="row">
        <div class="col-md-4">
          <h5 class="text-uppercase1">CodingPikka</h5>
          <p class="mb-0">© {{ year }} {{ companyName }}</p>
          <p class="mb-0">All rights reserved.</p>
        </div>
        <div class="col-md-2 other-content">
          <h5 class="text-uppercase">Company</h5>
          <ul class="list-unstyled">
            <li><a href="#">About Us</a></li>
            <li><a href="#">Our Services</a></li>
            <li><a href="#">Privacy Policy</a></li>
          </ul>
        </div>
        <div class="col-md-2 other-content">
          <h5 class="text-uppercase">Get Help</h5>
          <ul class="list-unstyled">
            <li><a href="http://localhost:8080/#/inquiry">문의사항</a></li>
            <li><a href="http://localhost:8080/#/post">공지사항</a></li>
          </ul>
        </div>
        <div class="col-md-4">
          <h5 class="text-uppercase">Follow Us</h5>
          <a href="https://github.com/codingpikka" class="mr-3">
            <img src=" https://cdn-icons-png.flaticon.com/256/3291/3291667.png " alt="github" class="social-icon">
          </a>
        </div>
      </div>
    </div>
  </footer>
</template>

<script>
export default {
  name: "CustomFooter",
  data() {
    return {
      year: new Date().getFullYear(),
      companyName: "코딩피카"
    };
  }
};
</script>

<style scoped>
.footer {
  background-image: linear-gradient( 135deg, #C2FFD8 10%, #465EFB 100%);
  color: #febe98;
  width: 100%;
  padding: 2rem 0;
  margin-top: 50px;
}
.row {
  justify-content: space-evenly !important;
}
.footer .col-md-2,
.footer .col-md-3,
.footer .col-md-4 {
  padding: 0.5rem;
}
.footer a {
  color: #febe98;
  text-decoration: none;
}
.footer a:hover {
  color: #e1a77c;
  text-decoration: underline;
}
.footer .fab,
.footer .fas {
  font-size: 1.25rem;
}
.footer p,
.footer h5 {
  margin: 0.5rem 0;
}
.text-uppercase1 {
  font-family: 'PuradakGentleGothicR', sans-serif;
  color: #febe98;
  font-size: 36px;
  margin: 0.5rem 0;
}
.text-uppercase {
  font-family: 'LINESeedKR-Bd', sans-serif;
  font-size: 18px;
  color: #fd8e4c;
}
.text-light {
  font-family: 'LINESeedKR-Bd', sans-serif;
  font-size: 14px;
}
.list-unstyled {
  font-family: 'LINESeedKR-Bd', sans-serif;
  font-size: 14px;
}
.mb-0 {
  font-family: 'LINESeedKR-Bd', sans-serif;
  font-size: 12px;
  color: #999;
}
.social-icon {
  width: 35px;
  height: 35px;
}
.chat-button {
  background-color: yellow;
  color: black;
  border: none;
  padding: 10px 20px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
  margin: 4px 2px;
  cursor: pointer;
  border-radius: 8px;
}
.cursor-pointer {
  cursor: pointer;
}
@media (max-width: 992px) {
  .footer .other-content {
    display: none;
  }
}
</style>