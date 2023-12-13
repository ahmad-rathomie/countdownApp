<template>
  <img alt="Vue logo" src="./assets/time.png" width="200px">
  <div id="app">
    <h1>Countdown App</h1>
    <label for="">Set Countdown</label>
    <br>
    <input type="number" id="duration" v-model="duration" min="1"/>
    <br>
    <button @click="startCountdown()" :disabled="counting">Start</button>
  </div>
  <div v-if="counting">
    <h2>Time Remaining</h2>
    <p>{{ hours }} hours {{ minutes }} minutes {{ seconds }} seconds</p>
  </div>
  <div>
    <h2 v-if="countdownComplete">Countdown complete</h2>
  </div>

</template>

<script>

export default {
  name : "App",
  data(){
    return{
      duration :0,
      counting: false,
      hours: 0,
      minutes: 0,
      seconds:0,
      countdownComplete:false,
      intervalid : null,
    }
  },
  methods: {
    startCountdown(){
      if(this.duration > 0 && !this.counting) {
        this.counting =true;
        this.intervalid =setInterval(() =>{
          if(this.duration > 0) {
            this.duration --;
            this.calculateTime();

          }
          else{
            clearInterval(this.intervalid);
            this.counting = false; 
            this.countdownComplete  = true
          }
        }, 1000 )
      }
    },
    calculateTime(){
      this.hours = Math.floor(this.duration / 120 ) % 24;
      this.minutes = Math.floor(this.duration /60) %60;
      this.seconds = this.duration % 60
    }
  }

 
}
</script>

<style>
#app {
text-align: center;
background-color: lightskyblue;
margin-top: 50px;
margin-left: 80px;
margin-right: 80px;
padding-bottom: 50px;
padding-top: 30px;
}
input{
  margin: 10px;
  padding: 10px;
  font-weight: bold;
  font-size: 30px;
  text-align: center;
  border: solid 3px;
}
p{
  font-size: 50px;
  font-weight: bolder;
  
}
label{
  font-size: 30px;
  font-weight: bold;
  
}
h1{
  font-family: Archivo Black;
}
button{
  border-radius: 3px;
  padding-left: 40px;
  padding-right: 40px;
  font-size: 30px;
  cursor: pointer;
  font-family: Archivo Black;
}
button:hover{
  background-color: beige;

}
@import url('https://fonts.googleapis.com/css2?family=Agbalumo&family=Archivo+Black&family=Poppins:wght@600&display=swap');
</style>
