<template>
  <div class="wrapper">
    <div class="blum-container">
      <div class="blum-header">
        <div class="blum-icon">🟦</div>
        <div class="blum-username">angelinachuspankik</div>
      </div>
      <div class="blum-main">
        <div class="blum-balance">Clicks: {{ clickCount }}</div>
        <div class="blum-box" @click="incrementClick">
          <p class="blum-box__text">Start game</p>
        </div>
      </div>
      <div class="blum-bottom">
        <button class="blum-button" @click="dropGame">Drop game</button>
        <div class="blum__quests">
          <div class="blum__quests-quest">
            <img src="" alt="a" />
            <p class="blue__quest-text">Home</p>
          </div>
          <div class="blum__quests-quest">
            <img src="" alt="a" />
            <p class="blue__quest-text">Home</p>
          </div>
          <div class="blum__quests-quest">
            <img src="" alt="a" />
            <p class="blue__quest-text">Home</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "MainPage",
  data() {
    return {
      clickCount: 0,
    };
  },
  methods: {
    incrementClick() {
      this.clickCount++;
      this.updateClickCount();
    },
    dropGame() {
      alert("10 лет тюрми");
      this.clickCount = 0;
    },
    async getClickCount() {
      try {
        let response = await fetch("get_click_count.php");
        let data = await response.json();
        this.clickCount = data.count;
      } catch (error) {
        console.error("Error fetching click count:", error);
      }
    },
    async updateClickCount() {
      try {
        await fetch("update_click_count.php", {
          method: "POST",
          headers: {
            "Content-Type": "application/json",
          },
          body: JSON.stringify({ count: this.clickCount }),
        });
      } catch (error) {
        console.error("Error updating click count:", error);
      }
    },
  },
  mounted() {
    this.getClickCount();
  },
};
</script>

<style scoped>
.wrapper {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  height: 100vh;
  background: #282c34;
  color: white;
  padding: 20px;
  box-sizing: border-box;
}

.blum-container {
  display: flex;
  flex-direction: column;
  justify-content: space-between; /* Add this line to push blum-bottom to the bottom */
  align-items: center;
  background: #1e1e2d;
  color: white;
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.5);
  width: 100%;
  max-width: 400px; /* Optional, to restrict the max width of the container */
  height: 100%;
}

.blum-header {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  margin-bottom: 20px;
}

.blum-icon {
  font-size: 40px;
  margin-right: 10px;
}

.blum-username {
  font-size: 28px;
}

.blum-balance {
  font-size: 42px;
  margin: 10px 0;
}

.blum-button {
  background: #4caf50;
  color: white;
  border: none;
  padding: 30px 120px;
  border-radius: 5px;
  cursor: pointer;
}

.blum-button:hover {
  background: #45a049;
}

.blum__quests {
  margin-top: 25px;
  display: flex;
  justify-content: center;
  gap: 30px;
}

.blum__quests-quest {
}

.blue__quest-text {
}

.blum-box {
  border-radius: 50%;
  margin: 20px;
  width: 300px;
  height: 300px;
  background-color: rgb(73, 74, 73);
  position: relative;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
}

.blum-box__text {
  font-size: 20px;
  color: white;
}
</style>
