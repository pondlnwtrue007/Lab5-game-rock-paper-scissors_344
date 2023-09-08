<template>
<div>
  <h1>เป่า ยิ้ง ฉุบ</h1>

  <div class="image-container">
    <img :src="playerImgUrl" alt="Player choice" />
    <p>Player</p>
  </div>

  <div class="image-container">
    <img :src="computerImgUrl" alt="Computer choice" />
    <p>AI</p>
  </div>

  <div class="buttons-container">
    <button @click="playGame('rock')">ค้อน</button>
    <button @click="playGame('paper')">กระดาษ</button>
    <button @click="playGame('scissors')">กรรไกร</button>
    <button @click="playGame('love')">หัวใจ</button>
  </div>

  <p>{{ result }}</p>
  <p>Score: Player - {{ playerScore }} | AI - {{ aiScore }}</p>
  <button @click="resetGame">เริ่มเกมใหม่</button>
</div>


</template>

<script setup>
import { ref } from 'vue';

const playerImgUrl = ref('https://github.com/pondlnwtrue007/Lab05-Create-a-rock-paper-scissors-game_344/blob/master/src/assets/player.png?raw=true');
const computerImgUrl = ref('https://github.com/pondlnwtrue007/Lab05-Create-a-rock-paper-scissors-game_344/blob/master/src/assets/ai.png?raw=true');
const result = ref('');
const playerScore = ref(0);
const aiScore = ref(0);

const choices = {
  rock: 'https://github.com/pondlnwtrue007/Lab05-Create-a-rock-paper-scissors-game_344/blob/master/src/assets/rockv1.png?raw=true',
  paper: 'https://github.com/pondlnwtrue007/Lab05-Create-a-rock-paper-scissors-game_344/blob/master/src/assets/paperv1.png?raw=true',
  scissors: 'https://github.com/pondlnwtrue007/Lab05-Create-a-rock-paper-scissors-game_344/blob/master/src/assets/scissorsv1.png?raw=true',
  love: 'https://github.com/pondlnwtrue007/Lab05-Create-a-rock-paper-scissors-game_344/blob/master/src/assets/love.png?raw=true'
};

const playGame = (playerChoice) => {
  playerImgUrl.value = choices[playerChoice];

  const computerChoice = ['rock', 'paper', 'scissors', 'love'][Math.floor(Math.random() * 4)]; // แก้ไขเพื่อให้ AI สามารถเลือก love ได้
  computerImgUrl.value = choices[computerChoice];

  if (playerChoice === computerChoice) {
    result.value = 'Draw!';
  } else if (
    (playerChoice === 'rock' && computerChoice === 'scissors') ||
    (playerChoice === 'paper' && computerChoice === 'rock') ||
    (playerChoice === 'scissors' && computerChoice === 'paper') ||
    (playerChoice === 'love')
  ) {
    result.value = 'You win!';
    playerScore.value++;
  } else {
    result.value = 'You lose!';
    aiScore.value++;
  }
};


const resetGame = () => {
  playerImgUrl.value = 'https://github.com/pondlnwtrue007/Lab05-Create-a-rock-paper-scissors-game_344/blob/master/src/assets/player.png?raw=true';
  computerImgUrl.value = 'https://github.com/pondlnwtrue007/Lab05-Create-a-rock-paper-scissors-game_344/blob/master/src/assets/ai.png?raw=true';
  result.value = '';
  playerScore.value = 0;
  aiScore.value = 0;
};
</script>


<style >
body {
  background-color: #000000; 
}
.image-container {
  position: relative;
  width: 100px;
  display: inline-block;
  margin: 10px 20px; /* ปรับระยะห่างของรูปภาพและชื่อ */
}

div {
  text-align: center;
}

.image-container p {
  font-size: 1.5rem;
  margin: 10px 0; 
  color: #D2691E; 
}


.image-container img {
  width: 100%;
  height: auto;
}

.image-container span {
  display: block;
  margin-top: 10px;
  background: transparent; /* ถ้าคุณไม่ต้องการพื้นหลังข้างหลังชื่อ */
}




/* ปรับหน้าตาของ div หลัก */
div {
  text-align: center; /* ตั้งค่าการจัดแนวข้อความและเนื้อหาให้อยู่กึ่งกลาง */

}

h1 {
  font-size: 2rem; /* ตั้งค่าขนาดฟอนต์ */
  color: #D2691E; /* สีส้มเข้ม */
  margin-bottom: 20px; /* กำหนดระยะห่างจากปุ่มด้านล่าง */
}

p {
  font-size: 2rem; /* ตั้งค่าขนาดฟอนต์ */
  color: #D2691E; /* สีส้มเข้ม */
}

button {
  font-size: 1.2rem; /* ตั้งค่าขนาดฟอนต์ของปุ่ม */
  margin: 10px; /* กำหนดระยะห่างระหว่างปุ่ม */
  padding: 10px 20px; /* กำหนดขนาดและรูปร่างของปุ่ม */
  background-color: #FFD700; /* สีปุ่มเป็นสีทอง */
  border: none; /* ซ่อนเส้นขอบของปุ่ม */
  cursor: pointer; /* เปลี่ยนเคอร์เซอร์เมื่อนำเมาส์ไปวางบนปุ่ม */
  transition: 0.3s; /* ตั้งค่าเวลาของการเปลี่ยนแปลง */
}

.buttons-container {
  margin-top: 20px; 
  display: block; /* ให้ปุ่มอยู่ในบรรทัดใหม่ */
}

button:hover {
  background-color: #FFA500; /* เปลี่ยนสีปุ่มเมื่อนำเมาส์ไปวางบนปุ่ม */
}


img {
  width: 100px; /* กำหนดความกว้างของรูปภาพ */
  height: 100px; /* กำหนดความสูงของรูปภาพ */
  margin: 20px; /* กำหนดระยะห่างระหว่างรูปภาพ */
}

p {
  font-size: 1.5rem; /* ตั้งค่าขนาดฟอนต์ของข้อความผลลัพธ์ */
  margin-top: 20px; /* กำหนดระยะห่างจากรูปภาพด้านล่าง */
}
 
</style>


