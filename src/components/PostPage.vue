<template>

  <body>
    <div>
      <header class="navbar">
        <div class="container">
          <p class="brand">HealthyKita.</p>
          <div class="nav-wrapper">
            <nav :class="['nav-list', { show: isMenuOpen }]" aria-label="Main Navigation">
              <router-link to="/home" class="nav-link">Home</router-link>
              <router-link to="/quiz/start" class="nav-link">Quiz</router-link>
            </nav>
            <button class="menu-toggle" @click="toggleMenu">
              <i class="fas fa-bars"></i>
            </button>
            <div class="user-profile" @click="toggleProfileDropdown">
              <img :src="require('/src/assets/download (1).jpg')" alt="Profile Picture" class="profile-picture" />
              <div :class="['dropdown-menu', { show: isProfileDropdownOpen }]">
                <div class="dropdown-content">
                  <div class="profile-card">
                    <div class="profile-card-header">
                      <img :src="require('/src/assets/download (1).jpg')" alt="Profile Picture"
                        class="card-profile-picture" />
                    </div>
                    <div class="notification-icon">
                      <router-link to="/notification"><i class="fa fa-bell"></i>
                        <span class="notification-count">3</span></router-link>

                    </div>
                    <span class="nickname">User.</span>
                    <div class="social-icons">
                      <a href="#" class="social-icon"><i class="fa-brands fa-facebook"></i></a>
                      <a href="#" class="social-icon"><i class="fa-brands fa-tiktok"></i></a>
                      <a href="#" class="social-icon"><i class="fa-brands fa-youtube"></i></a>
                      <a href="#" class="social-icon"><i class="fa-brands fa-google"></i></a>
                    </div>
                    <div class="profile-stats">
                      <div class="stat">
                        <span class="stat-number">350</span>
                        <span class="stat-label">Unggahan</span>
                      </div>
                      <div class="stat">
                        <span class="stat-number">200</span>
                        <span class="stat-label">Mengikuti</span>
                      </div>
                      <div class="stat">
                        <span class="stat-number">124K</span>
                        <span class="stat-label">Pengikut</span>
                      </div>
                    </div>
                    <div class="dropdown-divider"></div>
                    <router-link to="/profile/:username" class="dropdown-item">Profil</router-link>
                    <div class="dropdown-divider"></div>
                    <router-link to="/rank" class="dropdown-item">Daftar Peringkat</router-link>
                    <div class="dropdown-divider"></div>
                    <router-link to="/login" class="dropdown-item">Logout</router-link>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </header>
      <main class="content">
        <div class="tweet">
          <div class="tweet-header">
            <div class="profile-pic">
              <img :src="require('/src/assets/download (1).jpg')" alt="Profile Picture">
            </div>
            <div class="user-info">
              <div class="user-header">
                <span class="name">
                  Username
                  <i class="fa-solid fa-hand-holding-medical verified-icon"></i>
                  <button class="btn-follow" @click="toggleFollow">
                    {{ isFollowing ? 'Batal Mengikuti' : 'Ikuti' }}
                  </button>
                </span>
                <span class="username">@USername</span>
              </div>
            </div>
          </div>
          <div class="tweet-content">
            <span class="title">Title</span>
            <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et
              dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex
              ea commodo consequat. <span class="hashtag">#tes</span></p>
          </div>
          <div class="tweet-footer">
            <span class="date-time">11:30 PM · 21/03/2030 · 987K Views</span>
          </div>
          <div class="tweet-actions">
            <div class="action">
              <i class="fa-solid fa-comment"></i> 45K
            </div>
            <div class="action">
              <i class="fas fa-heart"></i> 91K
            </div>
            <div class="action">
              <i class="fas fa-share"></i>
            </div>
          </div>
          <div class="comment-section">
            <div class="comment-input-wrapper">
              <input type="text" class="comment-input" placeholder="Add a comment..." v-model="newComment">
              <button class="post-btn" @click="postComment">
                {{ isPost ? 'Terunggah' : 'Unggah' }}
              </button>
            </div>
          </div>
          <div class="non-comment-text">
            <h3>Belum Ada Komentar</h3>
          </div>
        </div>
      </main>

    </div>
  </body>
</template>


<script>
export default {
  data() {
    return {
      isProfileDropdownOpen: false,
      isMenuOpen: false,
      isFollowing: false,
      isPost: false,
    };
  },
  methods: {
    toggleProfileDropdown() {
      this.isProfileDropdownOpen = !this.isProfileDropdownOpen;
    },
    toggleMenu() {
      this.isMenuOpen = !this.isMenuOpen;
    },
    toggleFollow() {
      this.isFollowing = !this.isFollowing;
    },
    postComment() {
      this.isPost = !this.isPost;
    },
    handleClickOutside(event) {
      const profileDropdown = this.$el.querySelector(".user-profile");
      const menuDropdown = this.$el.querySelector(".nav-wrapper");
      if (
        profileDropdown &&
        !profileDropdown.contains(event.target) &&
        this.isProfileDropdownOpen
      ) {
        this.isProfileDropdownOpen = false;
      }
      if (
        menuDropdown &&
        !menuDropdown.contains(event.target) &&
        this.isMenuOpen
      ) {
        this.isMenuOpen = false;
      }
    },
  },
  mounted() {
    document.addEventListener("click", this.handleClickOutside);
  },
  beforeUnmount() {
    document.removeEventListener("click", this.handleClickOutside);
  },
};
</script>


<style scoped>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.title {
  font-weight: bold;

  font-size: large;
}

.notification-icon {
  position: absolute;
  top: 23px;
  right: 23px;
  font-size: 20px;
  color: #fff;
  background-color: #188754;
  border-radius: 50%;
  width: 30px;
  height: 30px;
  display: flex;
  align-items: center;
  justify-content: center;
  box-shadow: 0px 4px 6px rgba(0, 0, 0, 0.1);
  cursor: pointer;
  transition: transform 0.2s ease;
}

.notification-count {
  position: absolute;
  top: -5px;
  right: -5px;
  background: #fff;
  color: #e74c3c;
  font-size: 12px;
  border-radius: 50%;
  width: 15px;
  height: 15px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-weight: bold;
}

.notification-icon:hover {
  transform: scale(1.1);
}

.notification-icon:active {
  transform: scale(0.95);
}

body {
  background-color: #F5FFFA;
  color: black;
  font-family: 'Quicksand', sans-serif;
  height: 100vh;
  overflow-x: hidden;
}

/* Navbar */
.navbar {
  background-color: #188754;
  padding: 2rem 0;
  position: sticky;
  top: 0;
  z-index: 100;
}

.navbar .container {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 90%;
  max-width: 1200px;
  margin: 0 auto;
}

.brand {
  color: white;
  font-size: 1.5rem;
  font-weight: bold;
  cursor: pointer;
}

.nav-wrapper {
  display: flex;
  align-items: center;
}

.nav-list {
  display: flex;
  gap: 1.5rem;
  background-color: #188754;
  list-style: none;

}

.nav-link {
  font-size: 1rem;
  color: white;
  padding: 10px 15px;
  border-radius: 999px;
  text-decoration: none;
  transition: background-color 0.3s ease, color 0.3s ease;
}

.nav-link:hover {
  color: black;
  background-color: white;
}

.menu-toggle {
  display: none;
  font-size: 1.5rem;
  color: white;
  background: transparent;
  border: none;
  cursor: pointer;

}

/* Profile Dropdown */
.user-profile {
  position: relative;
  cursor: pointer;
}

.profile-picture {
  width: 40px;
  height: 40px;
  border-radius: 50%;
  object-fit: cover;
  margin-left: 30px;
  transition: transform 0.3s ease;
}

.profile-picture:hover {
  transform: scale(1.1);
}

.dropdown-menu {
  position: absolute;
  top: 100%;
  right: 0;
  background-color: #188754;
  border-radius: 10px;
  min-width: 300px;
  min-height: 300px;
  z-index: 1000;
  padding: 16px;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.2);
  opacity: 0;
  transform: translateY(-10px);
  transition: opacity 0.3s ease, transform 0.3s ease;
  margin-top: 20px;
  pointer-events: none;
}

.dropdown-menu.show {
  opacity: 1;
  transform: translateY(0);
  pointer-events: auto;
  animation: fadeInSlideDown 0.3s ease-in-out forwards;
}

.dropdown-content {
  background-color: white;
  border-radius: 10px;
  padding: 16px;
  color: black;
}

.profile-card {
  text-align: center;
  flex-direction: column;
}

.card-profile-picture {
  width: 80px;
  height: 80px;
  border-radius: 50%;
  object-fit: cover;
  border: 2px solid #ddd;
}

.nickname {
  font-size: 1.2em;
  font-weight: bold;
}

.social-icons {
  display: flex;
  justify-content: center;
  gap: 10px;
  margin: 10px 0;
}

.social-icon {
  color: black;
  font-size: 1.2rem;
  transition: color 0.3s ease, transform 0.3s ease;
}

.social-icon:hover {
  color: #188754;
  transform: scale(1.1);
}

.dropdown-item {
  display: block;
  padding: 10px;
  text-align: center;
  text-decoration: none;
  color: black;
  border-radius: 5px;
  margin: 5px 0;
  transition: background-color 0.3s ease;
}

.dropdown-item:hover {
  background-color: #f1f1f1;
}


/* Stats Section */
.profile-stats {
  display: flex;
  justify-content: space-around;
  margin-bottom: 30px;
}

.stat {
  text-align: center;
}

.stat-number {
  font-weight: bold;
  font-size: 18px;
  display: block;
}

.stat-label {
  font-size: 14px;
  color: #999;
}

/* Tweet Section */
.content {
  display: flex;
  justify-content: center;
  align-items: flex-start;
  min-height: 80vh;
  padding: 20px;
  box-sizing: border-box;
}

.tweet {
  /* background-color: #fff;
  
  border-radius: 10px;
  width: 600px;
  padding: 50px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1); */
  width: 90%;
  max-width: 700px;
  height: auto;
  min-height: 400px;
  border: 1px solid #e1e8ed;
  margin: 20px auto;
  padding: 30px;
  background-color: white;
  border-radius: 10px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  font-size: 1.1rem;
  line-height: 1.6;
}

.tweet-header {
  display: flex;
  align-items: flex-start;
  gap: 15px;
  margin-bottom: 15px;
  width: 100%;
}
.profile-pic{
  flex-shrink: 0;
}

.profile-pic img {
  width: 50px;
  height: 50px;
  border-radius: 50%;
  object-fit: cover;
}

.user-info {
  flex: 1;
  display: flex;
  flex-direction: column;
}

.user-header {
  display: flex;
  flex-direction: column;
  gap: 2px;
}

.name {
    display: flex;
  align-items: center;
  font-weight: bold;
  font-size: 16px;
}

.username {
  color: #657786;
  font-size: 14px;
}
.verified-icon {
  color: #188754;
  margin-left: 8px;
  font-size: 14px;
}
/* .user-info .name {
  display: flex;
  align-items: center;
  font-weight: bold;
  font-size: 16px;
  flex-wrap: wrap;
} */

/* .user-info .verified-icon {
  color: #188754;
  font-size: 14px;
  margin-left: 10px;
} */

/* .user-info .username {
  display: block;
  font-size: 14px;
  color: #657786;
} */

.tweet-content {
  width: 100%;
  word-wrap: break-word;
  overflow-wrap: break-word;
  margin: 15px 0;
}

.tweet-content p {
  font-size: 15px;
  line-height: 1.5;
  color: #14171a;
}

.hashtag {
  color: #1DA1F2;
  cursor: pointer;
}

.date-time {
  display: block;
  font-size: 12px;
  color: #657786;
  margin-top: 10px;
  border-top: 1px solid #e1e8ed;
  padding-top: 10px;
}

.tweet-actions {
  display: flex;
  border-bottom: 1px solid #e1e8ed;
  align-items: center;
  margin-top: 3px;
  margin-bottom: 10px;
  padding-bottom: 10px;
  font-size: 14px;
}

.action {
  display: flex;
  align-items: center;
  color: #657786;
  cursor: pointer;
  margin-right: 20px;
}

.action i {
  margin-right: 5px;
}

.action:hover {
  color: #1DA1F2;
}

.comment-section {
  width: 100%;
  margin: 15px 0;
  padding-bottom: 10px;
  border-bottom: 1px solid #e1e8ed;

}

.comment-input-wrapper {
  display: flex;
  align-items: center;
  width: 100%;
  background-color: #f5f8fa;
  border-radius: 30px;
  padding: 5px 10px;
  box-sizing: border-box;
}



.comment-input {
  flex: 1;
  padding: 8px;
  margin-right: 10px;
  border: none;
  background-color: transparent;
  border-radius: 30px;
}

.post-btn {
  background-color: #188754;
  color: white;
  padding: 8px 20px;
  border-radius: 20px;
  font-size: 0.9rem;
  cursor: pointer;
  transition: background-color 0.3s ease, transform 0.2s ease;
  margin-left: 10px;
  border: none;
}

.post-btn:hover {
  background-color: #145a40;
  transform: scale(1.05);
}

.post-btn:active {
  transform: scale(0.95);
}

.comment-input::placeholder {
  color: #657786;
}

.non-comment-text {
  margin-top: 30px;
  text-align: center;
}

.btn-follow {
  background-color: #188754;
  color: white;
  padding: 5px 15px;
  border-radius: 20px;
  font-size: 14px;
  cursor: pointer;
  transition: all 0.3s ease;
  border: none;
  margin-left: 10px;
  /* background-color: #188754;
  color: white;
  padding: 5px 15px;
  border-radius: 20px;
  font-size: 14px;
  border: none;
  cursor: pointer;
  margin-left: auto;
  transition: all 0.3s ease; */
}

.btn-follow:hover {
  background-color: #134734;
  transform: scale(1.05);
}

.btn-follow:active {
  transform: scale(0.95);
}

@keyframes fadeInSlideDown {
  from {
    opacity: 0;
    transform: translateY(-10px);
  }

  to {
    opacity: 1;
    transform: translateY(0);
  }
}
@media (max-width: 480px) {
  .tweet-header {
    gap: 10px;
  }
  
  .profile-pic img {
    width: 40px;
    height: 40px;
  }
  
  .name {
    font-size: 14px;
  }
  
  .username {
    font-size: 12px;
  }
  
  .btn-follow {
    padding: 4px 12px;
    font-size: 12px;
  }
}
@media (max-width: 941px) {
  .container {
    flex-direction: column;
    align-items: flex-start;
  }

  .nav-list {
    display: none;
    flex-direction: column;
    width: 100%;
    background-color: #188754;
    box-shadow: 0 2px 5px rgba(0, 0, 0, 0.2);
    animation: fadeInSlideDown 0.3s ease-in-out forwards;
  }

  .nav-list.show {
    display: flex;
  }

  .menu-toggle {
    display: block;
  }

  .profile-container {
    width: 100%;
    padding: 20px;
  }

  .profile-details {
    flex-direction: column;
    align-items: center;
    text-align: center;
  }

  .profile-details .profile-picture {
    margin-bottom: 20px;

  }

}

@media (max-width: 941px) {
  .container {
    flex-direction: row;
    align-items: center;
    justify-content: space-between;
  }

  .nav-wrapper {
    flex-direction: row;
    width: auto;
    align-items: center;
  }

  .nav-list {
    position: absolute;
    top: 100%;
    left: 0;
    flex-direction: column;
    margin-left: 0;
    width: 100%;
    display: none;
    background-color: #188754;
    z-index: 100;
    padding: 1rem;
    box-shadow: 0 2px 5px rgba(0, 0, 0, 0.2);

  }

  .nav-list.show {
    display: flex;
  }

  .nav-link {
    display: block;
    width: 100%;
    text-align: left;
    padding: 0.7rem 1rem;
    border-radius: 40px;

  }

  .brand {
    margin-left: 0px;
    margin-bottom: 0;
  }

  .user-profile {
    margin-right: -20px;

  }

  .menu-toggle {
    display: block;
    margin-left: 0;
  }

  .dropdown-menu {
    margin-top: 20px;
  }
}

@media (max-width: 768px) {
  .tweet {
    width: 95%;
    padding: 20px;
    margin: 10px auto;
  }

  .btn-follow {
    margin-left: 5px;
    padding: 4px 12px;
    font-size: 13px;
  }

  .tweet-content p {
    font-size: 14px;
  }

  .post-btn {
    padding: 6px 15px;
    font-size: 0.85rem;
  }

  .comment-input {
    font-size: 14px;
  }
}

@media (max-width: 480px) {
  .tweet {
    width: 100%;
    padding: 15px;
    margin: 5px auto;
  }

  .tweet-header {
    margin-bottom: 10px;
  }

  .profile-pic img {
    width: 40px;
    height: 40px;
  }

  .user-info .name {
    font-size: 14px;
  }

  .user-info .username {
    font-size: 12px;
  }

  .btn-follow {
    padding: 3px 10px;
    font-size: 12px;
    margin-left: 5px;
  }

  .tweet-content p {
    font-size: 13px;
  }

  .comment-input-wrapper {
    padding: 3px 8px;
  }

  .post-btn {
    padding: 5px 12px;
    font-size: 0.75rem;
  }

  .non-comment-text {
    margin-top: 20px;
    font-size: 14px;
  }
}

.navbar {
  background-color: #188754;
  padding: 1rem 0;
  position: sticky;
  top: 0;
  z-index: 100;
}
</style>
