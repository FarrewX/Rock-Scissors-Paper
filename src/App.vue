<template>
  <h1>เกมเป่ายิ่งฉุบ</h1>
    <div>
      <img :src="playerChoiceImg" class="choice-image" alt="รูปผู้เล่น">
      <img :src="botChoiceImg" class="indent choice-image" alt="รูปบอท"><br><br>
    </div>
    <div class="choices">
      <button @click="play(this.choices[Math.floor(Math.random() * 4)])">เป่ายิ่งงงง ฉุบ</button>
    </div>
    <div class="result">
      <p>ผล: {{ result }}</p>
      <p>คะแนนของคุณ : คะแนนของบอท </p>
      <p>{{ playerScore }} : {{ botScore }}</p>
    </div>
    <button @click="reset">Reset</button>&nbsp;
    <button @click="reloadPage">Reload Page</button>
</template>



<script>
export default {
    el: '#app',
    data() {
      return {
        choices: ['rock', 'scissors', 'paper', 'heart'],
        result: '',
        playerScore: 0,
        botScore: 0,
        playerChoiceImg: 'src/images/default.png', // รูปเริ่มต้นของผู้เล่น
        botChoiceImg: 'src/images/default.png', // รูปเริ่มต้นของบอท
      };
    },
    methods: {
        play(playerChoice) {
            const botChoice = this.choices[Math.floor(Math.random() * 4)];
            this.showResult(playerChoice, botChoice);
            this.playerChoiceImg = `src/images/${playerChoice}.png`; // เปลี่ยนรูปผู้เล่น
            this.botChoiceImg = `src/images/${botChoice}.png`; // เปลี่ยนรูปบอท
        },//public/images
        showResult(playerChoice, botChoice) {
            if (playerChoice === botChoice) {
                this.result = 'เสมอ';
            } else if (
                (playerChoice === 'rock' && botChoice === 'scissors') ||
                (playerChoice === 'scissors' && botChoice === 'paper') ||
                (playerChoice === 'paper' && botChoice === 'rock') ||
                (playerChoice === 'heart' && botChoice !== 'heart')
            ) {
                this.result = 'ชนะ';
                this.playerScore++;
            } else {
                this.result = 'แพ้';
                this.botScore++;
            }
        },
        reset() {
          this.playerScore = 0;
          this.botScore = 0;
        },

        reloadPage() {
          window.location.reload();
        },

        mounted() {
          let recaptchaScript = document.createElement('script')
          recaptchaScript.setAttribute('src', 'https://cdn.jsdelivr.net/npm/vue/dist/vue.js')
          document.head.appendChild(recaptchaScript)
        }
    },
};

</script>
