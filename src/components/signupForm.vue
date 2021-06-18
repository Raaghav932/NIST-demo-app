<template>
  <h1>Welcome to the online store!</h1>

  <img src="https://cdn.geekwire.com/wp-content/uploads/2020/02/amzngo1.jpeg" width="400" height="200">



  <!-- This is the form and it also prevents the 'standard' from submission -->
  <form @submit.prevent="handleSubmit">
    <label>Email:</label>
    <input type="email" required v-model="email">

    <label>Password:</label>
    <input type="password" required v-model="password">

    <div v-if = "passwordError" class ="error">{{ passwordError }}</div>

    <label>Role:</label>
    <select v-model='membership'>
      <option value="free">Free Member</option>
      <option value="paid">Paid Member</option>
    </select>

    <div class="terms">
      <input type="checkbox" v-model="terms" required>
      <label>Accept Terms and Conditions </label>
    </div>

    <label>How did you hear about us</label>
    <div>
      <input type="checkbox" value = "Ads" v-model="referral">
      <label>Advertisement</label>
    </div>
    <div>
      <input type="checkbox" value = "Web" v-model="referral">
      <label>Web Search</label>
    </div>
        <div>
      <input type="checkbox" value = "Tv" v-model="referral">
      <label>Television Advertisement</label>
    </div>


    <!-- this is the functionality for the purchases -->

    <label>What do you want to purchase:</label>
    <input type="text" v-model="tempPurch" @keyup.enter="addPurch">
    <div v-for = "purchase in purchases" :key="purchase" class = 'pill'>
      <span @click="deletePurchase(purchase)">{{ purchase }}</span>
    </div>
    <button type="submit" disabled style="display: none" aria-hidden="true"></button>
    <div class = "submit">
      <button>Create an Account</button>
    </div>

  </form>

  <p>Email: {{ email }}</p>
  <p>Password: {{ password }}</p>
  <p>Role: {{ membership }} </p>
  <p>Terms accepted: {{ terms }} </p>
  <p>Referrals: {{ referral }} </p>
</template>

<script>

export default {
  data(){
    return{
      email: '',
      password: '',
      membership: 'free',
      terms: false,
      referral:[],
      tempPurch: '',
      purchases: [],
      passwordError: '',
    }
  },
  
  //These are the methods for the pruchases and when the form submits

  methods:{
    addPurch(e){
      if(this.tempPurch){
        if(!this.purchases.includes(this.tempPurch)){
          console.log("Adding purchase")
          this.purchases.push(this.tempPurch)
          this.tempPurch = ''
        }
      }
    },

    deletePurchase(purchase){
      this.purchases = this.purchases.filter((item) => {
        return purchase !== item
      })
    },

    handleSubmit(){
      console.log("form submited")
      this.passwordError = this.password.length > 5 ? '' : 'Password must be at least 6 chars long'
      if(!this.passwordError){
        console.log("Email: ", this.email)
        console.log("Password: ", this.password)
        console.log("Membership: ", this.role)
        console.log("Referral: ", this.skills)
        console.log("Therms: ", this.terms)
        window.alert("Thank you for your order")
      }
    }

  }
}
</script>


<!-- This is the styling -->

<style>
form{
  max-width: 420px;
  margin: 30px auto;
  background: white;
  text-align: left;
  padding: 40px;
  border-radius: 10px;
}
label{
  color: #aaa;
  display: inline-block;
  margin: 25px 0 15px;
  font-size: 0.6em;
  text-transform: uppercase;
  letter-spacing: 1px;
  font-weight: bold;
}
input, select{
  display: block;
  padding: 10px 6px;
  width: 100%;
  box-sizing: border-box;
  border: none;
  border-bottom: 1px solid #ddd;
  color: #555;
}

input[type="checkbox"]{
  display: inline-block;
  width: 16px;
  margin: 0 10px 0 0;
  position: relative;
  top: 2px;
}
.pill{
  display: inline-block;
  margin: 20px 10px 0 0;
  padding: 6px 12px;
  background: #eee;
  border-radius: 20px;
  letter-spacing: 1px;
  font-weight: bold;
  color: #777;
  cursor: pointer;
}

button{
  background: darkblue;
  border: 0;
  padding: 10px 20px;
  margin-top: 20px;
  color: white;
  border-radius: 20px;
  cursor: pointer;
}

.submit{
  text-align: center;
}

.error{
  color: #ff0062;
  margin-top: 10px;
  font-size: 0.8em;
  font-weight: bold;
}
</style>











