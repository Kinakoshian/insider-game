<template>
  <div class="regist-player">
    <ul class="player-list">
      <li v-for="(player, index) in players" class="player-item">
        <label class="player-num">Player {{ index }} : </label>
        <input v-model="player.name" placeholder="Name" class="player-name">
      </li>
    </ul>
    <div class="btn-container">
      <button class="btn btn-primary" v-on:click="addPlayer()">追加</button>
      <button class="btn btn-primary" v-on:click="regist()">送信</button>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: 'RegistPlayer',
  data() {
    return {
      players: [
        { name: ''},
        { name: ''},
        { name: ''},
        { name: ''},
      ],
    }
  },
  methods: {
    addPlayer() {
      this.players.push({ name: ''});
    },
    async regist() {
      let postData = [];
      this.players.forEach(player =>{
        postData.push(player.name);
      })

      await axios
        .post(
          "https://6rdb8uj2l8.execute-api.ap-northeast-1.amazonaws.com/dev/regist",
          {
            players: postData
          }
        )
        .then(res => {
          this.$store.dispatch("updateGameId", res.data.body.gameId);

          this.$router.push({ name: 'ConfirmRole', query: { gameId: res.data.body.gameId }})
        })
        .catch(() => {
          alert("通信に失敗しました。");
        });
    }
  }
}
</script>

<style>
.player-list {
  margin-bottom: 64px;
}
.player-item {
  margin-bottom: 24px;
}
.player-num {
  display: inline-block;
  vertical-align: bottom;
  line-height: 18px;
  padding: 4px 16px 4px 0;
  border-bottom: 1px solid #f79;
  font-size: 14px;
  color: #f79;
}
.player-name {
  display: inline-block;
  vertical-align: bottom;
  padding: 4px;
  line-height: 20px;
  font-size: 18px;
  border: none;
  border-bottom: 1px solid #f79;
  background-color: transparent;
  color: #f79;
  width: 240px;
  text-align: right;
  font-weight: bold;
}
.player-name::placeholder {
  color: #bbb;
}
.player-name:focus {
  outline: none;
}
.btn-container {
  text-align: center;
}
.btn-primary {
  font-size: 14px;
  border: none;
  line-height: 20px;
  padding: 12px;
  width: 160px;
  background-color: #f79;
  color: #fff;
  margin: 0 16px;
  border-radius: 50px;
  font-weight: bold;
  outline: none;
  box-shadow: none;
}
.btn-primary:hover {
  box-shadow: 0 0 12px 0 rgba(255, 100, 120, .5);
  cursor: pointer;
}
</style>
