<template>
  <div class="home container-fluid">
    <h1>BattleCards</h1>
    <div class="row">
      <div class="col-6 offset-3 align-items-center">
        <form v-on:submit.prevent="startGame" class="">
          Enter Name: <input type="text" v-model="game.gameConfig.playerName" placeholder="Your Name"> <br># of
          Opponents: <input type="number" v-model="game.gameConfig.opponents" placeholder="# of Opponents"><br> Deck #:
          <input type="number" v-model="game.gameConfig.set" placeholder="Set #">
          <button @click="startGame">Start</button>
          <button type="button" @click="gameList">Games</button>

        </form>
      </div>
    </div>
    <div>
      <p v-for="game in gamesList">
        <!-- Game ID: {{game._id}} -->
        {{game.players[0].name}} vs. {{game.players[1].name}}
        <button @click="selectGame(game.id)">Continue</button>
      </p>
    </div>
  </div>
</template>

<script>
  import router from '../router.js'

  export default {
    name: "Home",
    data() {
      return {
        game: {
          gameConfig: {
            playerName: "",
            opponents: 1,
            set: 1
          }
        }
      }
    },
    computed: {
      gamesList() {
        return this.$store.state.games
      },
      singleGame() {
        return this.$store.state.game
      }
    },
    components: {

    },
    methods: {
      startGame() {
        this.$store.dispatch('createGame', this.game)
      },
      gameList() {
        this.$store.dispatch('listGames')
      },
      goToGame() {
        router.push({ name: 'game' })
      },
      selectGame(gameId) {
        this.$store.dispatch('getGame', gameId)
      }

    }
  }

</script>

<style>
  body {
    background-color: black;
    height: 100vh;
    color: antiquewhite;
  }

  .home {
    color: antiquewhite;
  }
</style>