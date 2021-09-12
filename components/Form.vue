<template>
<div>
    <h1>Register Now!!!</h1>

    <b-form class="container" @submit="sendOtp">
        <b-form-group label="Phone No.:" description="We will not share your phone no. with anyone.">
            <b-form-input type="tel" v-model="form.phone" pattern="[0-9]{10}">
            </b-form-input>
        </b-form-group>
        <b-button type="submit" variant="success">Submit</b-button>

    </b-form>
</div>
  
</template>

<script>
//import axios from 'axios'
export default {
    name: 'Form',
    data(){
        return{
            form:{
              phone: '',
              //res = null
            }
        }
    },

    methods:{
        OnSubmit(){
            this.$emit('phone_no', this.form.phone)
        },

        sendOtp(){
            try{
        const res = fetch('http://13.127.45.20:5001/sendOTP', {
            method: "POST",
            headers:{
                "Content-Type": "application/json"
            },
            body: JSON.stringify({
                number: this.form.phone
            }),
        });

        const data = res.json();

        if(res.status === 202){
            console.log(data.message);
        }
        else{
            console.log(data.message);
        }
        }
        catch(err){
            console.warn(err);
        }
        }
    },

    /* async created(){
        //e.preventDefault();
        try{
        const res = await fetch('http://13.127.45.20:5001/sendOTP', {
            method: "POST",
            headers:{
                "Content-Type": "application/json"
            },
            body: JSON.stringify({
                number: 9150435380
            }),
        });

        const data = await res.json();

        if(res.status === 202){
            console.log(data.message);
        }
        else{
            console.log(data.message);
        }
        }
        catch(err){
            console.warn(err);
        }


    } */

    /* async created(){
        const config={
            header : {
                Accept:"applications/json"
            },
            body: JSON.stringify({
                raw:{
                   number: this.form.phone
                }
                
            })
        };
        try{
            const output = await axios.post(`http://13.127.45.20:5001/sendOTP`, config);
            console.warn(output)
        
    }
    catch(err){
        console.warn(err);
    }

} */

}
</script>

<style>

</style>