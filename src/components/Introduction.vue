<template>
  <div class="introContainer" v-show="showIntro">
    <main class="intro question">How Well Do You Know Me?</main>
    <p class="intro info">To start the quiz, please enter your name and click proceed.</p>
    <input type="text" id="name" name="name" v-model="name" placeholder="Enter your name"/>
    <button type="button" id="proceed" @click="proceed" value="name">Proceed</button>
  </div>
  <Questions v-if="showIntro === false" :name="name"/>
</template>

<script>
  import Questions from "@/components/Questions";
  import Swal from "sweetalert2";

  export default {
    name: 'Introduction',
    components: { Questions },
    data() {
      return {
        showIntro: true,
        name: ''
      }
    },

    methods:  {
      proceed() {
        if(this.name === '') {
          Swal.fire(
            'Error',
            "You did not enter you name",
            'error'
          )
        }
        else {
          this.showIntro = false;
        }
      }
    }
  }
</script>

<style lang="scss" scoped>
$color: white;

  .introContainer {
    height: 100vh;
    display: flex;
    flex-direction: column;
    flex-wrap: wrap;
    align-items: center;
    justify-content: center;
  }

  .intro {
    color: $color;
    text-align: center;
    font-family: "Arial Hebrew", serif;

    &.question {
      font-size: 40px;
      margin: 30px auto;
    }

    &.info {
      font-size: 18px;
      font-style: italic;
    }
  }

  #name {
    border: transparent;
    border-radius: 5px;
    padding: 10px 45px 10px 4px;
    margin: 5px auto;
  }

  #proceed {
    border: transparent;
    border-radius: 5px;
    background-color: #4681f4;
    color: $color;
    padding: 5px 10px;
    font-size: 15px;
    cursor: pointer;
    margin: 10px auto;
  }
</style>
