<template>
  <form @submit.prevent="handleSubmit">
    <label> Email:</label>
    <input type="email" required v-model="email">

    <label> Password:</label>
    <input type="password" required v-model="password">
    <div v-if="passwordError" class="error">{{ passwordError }}</div>

    <label> Role:</label>
    <select v-model="role">
        <option value="Developer">Web Developer</option>
        <option value="Teacher">Teacher</option>
        <option value="Designer">Designer</option>
    </select>

    <label>Skills</label>
    <input type="text" v-model="tempSkill" @keyup="addSkill">
    <div v-for="(skill,index) in skills" :key="skill" class="pill">
    <span @click="deleteSkill(index)">{{ skill }}</span>
    </div>

    <div class="terms">
        <input type="checkbox" required v-model="terms">
        <label @click="terms=!terms">Accept terms and conditions</label>
    </div>

    <div class="submit">
        <button>
            Create an Account
        </button>
    </div>
  </form>

  <p>email: {{ email }}</p>
  <p>passowrd: {{ password }}</p>
  <p>role: {{ role }}</p>
  <p>terms: {{ terms }}</p>
  <p>skills: {{ skills }}</p>
</template>

<script>
export default {
    data() {
        return {
            email:'',
            password:'',
            role:'Developer',
            terms:false,
            tempSkill:'',
            skills:[],
            passwordError:''
        }
    },
    methods: {
        addSkill(e){
            var gelen=this.tempSkill.substring(0,this.tempSkill.length-1)
            if(e.key === ',' && gelen)
            {
                if(!this.skills.includes(gelen))
                {
                    this.skills.push(gelen)
                }
                this.tempSkill=''
            }
        },
        deleteSkill(index){
            this.skills.splice(index,1) //index in bulunduğu sıradan sonraki 1 elemanı diziden siler.
        },
        handleSubmit(){
           //validate password
            this.passwordError=this.password.length > 5 ? '' : 'Password must be at least 6 chars long'
            if (!this.passwordError) {
                console.log(this.email)
                console.log(this.password)
                console.log(this.role)
                console.log(this.terms)
                console.log(this.skills)
            }
        }
    },
}
</script>

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
    color: #777;
    display: inline-block;
    margin: 25px 0 15px;
    font-size: 0.6em;
    text-transform: uppercase;
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
    font-size: 12px;
    letter-spacing: 1px;
    font-weight: bold;
    color: #777;
    cursor:pointer;
}
button{
    background: #0b6dff;
    border: 0;
    padding: 10px 20px;
    margin-top: 20px;
    color: white;
    border-radius: 20px;
}
.submit{
    text-align: center;
}
.error{
    color:#ff0062;
    margin-top: 10px;
    font-size: 0.8em;
    font-weight: bold;
}
</style>