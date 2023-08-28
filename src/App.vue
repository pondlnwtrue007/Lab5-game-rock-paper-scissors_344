<template>
  <div>
    <h1>เป่า ยิ้ง ฉุบ</h1>
    <button @click="playGame('rock')">ค้อน</button>
    <button @click="playGame('paper')">กระดาษ</button>
    <button @click="playGame('scissors')">กรรไกร</button>
    <img :src="playerImgUrl" alt="Player choice" />
    <img :src="computerImgUrl" alt="Computer choice" />
    <p>{{ result }}</p>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const playerImgUrl = ref(new URL('./assets/default.png', import.meta.url).href);
const computerImgUrl = ref(new URL('./assets/default.png', import.meta.url).href);
const result = ref('');

const choices = {
  rock: './assets/rock.png',
  paper: './assets/paper.png',
  scissors: './assets/scissors.png',
};

const playGame = (playerChoice) => {
  playerImgUrl.value = new URL(choices[playerChoice], import.meta.url).href;
  
  const computerChoice = ['rock', 'paper', 'scissors'][Math.floor(Math.random() * 3)];
  computerImgUrl.value = new URL(choices[computerChoice], import.meta.url).href;
  
  if (playerChoice === computerChoice) {
    result.value = 'Draw!';
  } else if (
    (playerChoice === 'rock' && computerChoice === 'scissors') ||
    (playerChoice === 'paper' && computerChoice === 'rock') ||
    (playerChoice === 'scissors' && computerChoice === 'paper')
  ) {
    result.value = 'You win!';
  } else {
    result.value = 'You lose!';
  }
};
</script>
