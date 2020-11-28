<template>
  <div id="app">
    <section>
    <h2>Password Strength Checker</h2>
    <div class="input_container">
      <input type="password" placeholder="Password"  @input="HandlePasswordLength()" v-model="password"/>
    </div>
    <div class="condition_container">
      <p :class="{number_valid:contains_number}">Number</p>
      <p :class="{uppercase_valid:contains_uppercase}">Uppercase</p>
      <p :class="{lowercase_valid:contains_lowercase}">Lowercase</p>
    </div>
    <div class="valid_password_container" :class="{show_valid_password_container:valid_password}">
       <svg width="100%" height="100%" viewBox="0 0 140 100">
            <path class="tick" :class="{checked: valid_password }" 
                d="M10,50 l25,40 l95,-70" />
            </svg>
    </div>
  </section>
  <section class="footer">
    <p>Created by Muhaamad Zainal Arifin</p>
  </section>
  </div>
</template>


<script>
export default {
  name:'App',
  data : () => {
    return {
      password : null,
      password_length: 0,
      typed:false,
      contains_number:false,
      contains_lowercase:false,
      contains_uppercase:false,
      valid_password_length:false,
      valid_password:false
    }
  },
  methods:{
    HandlePasswordLength(){
      this.password_length = this.password.length
      this.valid_password_length > 7 ? this.valid_password_length = true : this.valid_password_length = false
      this.contains_lowercase = /[a-z]/.test(this.password)
      this.contains_number = /\d/.test(this.password)
      this.contains_uppercase = /[A-Z]/.test(this.password);

      // check if password valid
      if(this.contains_lowercase == true && this.contains_number == true){
        this.valid_password = false;
        if(this.contains_lowercase == true && this.contains_number == true){
          this.valid_password = true;
        }else{
          this.valid_password = false
        }
      }
    }
  }
}
</script>

<style>
@import url("https://fonts.googleapis.com/css?family=Montserrat:400,700");
html {
  box-sizing: border-box;
}

*,
*:before,
*:after {
  box-sizing: inherit;
  padding: 0;
  margin: 0;
}

body{
  font-family: 'Montserrat',sans-serif;;
  line-height: 1.3;
  letter-spacing: 1px;
  background-color: rgb(201, 201, 201);
}

input[type="password"]::input-placeholder{
  color:rgba(71,87,98,0.8)
}

#app {
  width: 350px;
  padding:10px;
  text-align: center;
  position: absolute;
  top:50%;
  left:50%;
  transform: translate(-50%,-50%);
}

h2{
  font-size: 25px;
  color:rgb(21, 22, 22);
  text-align: center;
}

.input_container {
  display: block;
  margin: 0 auto;
  width: 320px;
  height: auto;
  position: relative;
  border-radius: 4px;
  overflow: hidden;
  margin-bottom: 10px;
}

input[type="password"]{
  width: 320px;
  margin: 30px 0;
  border: 1px solid transparent;
  background-color: #eee;
  color: #475762;
  font-size: 15px;
  border-radius: 4px;
  padding: 12px 5px;
  overflow: hidden;
  outline: none;
  transition: all 0.1s;
}
input[type="password"]:focus{
  border: 1px solid #2196F3;
}

.password_length{
  padding:2px 10px;
  position: absolute;
  top: 10%;
  right:10px;
  transform: translateY(-50%);
  background-color: black;
  font-size:13px;
  display: none;
  transition: all 0.1s;
}

.valid_password_length{
  background-color: #00AD7C;
  color: rgba(255, 255, 255, 0.9);
}

.show_password_length{
  display: block;
}

.condition_container {
  display: block;
  margin: 10px auto;
  width: 320px;
  height: auto;


  -webkit-box-pack: justify;
          justify-content: space-between;
}

.condition_container p {
  width: 320px;
  height: auto;
  font-size: 12px;
  line-height: 1.2;
  text-align: left;
  padding: 10px;
  margin-top: 5px;
  border-radius: 2px;
  color: rgba(71, 87, 98, 0.8);
  background: -webkit-gradient(linear, left top, right top, color-stop(50%, #00AD7C), color-stop(50%, #eee));
  background: linear-gradient(to right, #00AD7C 50%, #eee 50%);
  background-size: 201% 100%;
  background-position: right;
  -webkit-transition: background .3s;
  transition: background .3s;
}
.lowercase_valid,
.number_valid,
.uppercase_valid{
  background-position: left !important;
  color: rgba(255, 255, 255, 0.9) !important;
}

.valid_password_container{
  display: block;
  margin: 10px auto;
  border-radius: 4px;
  position: relative;
  background: #00AD7C;
  width: 20px;
  height: 20px;
  visibility: hidden;
  opacity: 0;
}

.show_valid_password_container{
  visibility: visible;
  opacity: 1;
}

.tick{
  width: 100%;
  height: 100%;
  fill: none;
  stroke: white;
  stroke-width: 25;
  stroke-linecap: round;
  stroke-dasharray: 180;
  stroke-dashoffset: 180;
}
.checked{
  -webkit-animation: draw 0.5s ease forwards;
  animation: draw 0.5s ease forwards;
}

@-webkit-keyframes draw {
  to {
    stroke-dashoffset: 0;
  }
}

@keyframes draw {
  to {
    stroke-dashoffset: 0;
  }
}

</style>
