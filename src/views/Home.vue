<template>
  <div class="container">
    <form
      ref="form"
      @submit.prevent="sendEmail()"
    >
      <label>Name</label>
      <input
        v-model="from_name"
        type="text"
        name="from_name"
        placeholder="Your Name"
      >
      <label>Email</label>
      <input
        v-model="email"
        type="email"
        name="user_email"
        placeholder="Your Email"
      >
      <label>Message</label>
      <textarea
        v-model="message"
        name="message"
        cols="30"
        rows="5"
        placeholder="Message"
      />

      <input
        type="submit"
        value="Send"
      >
    </form>
  </div>
</template>

<script>
import emailjs from '@emailjs/browser';
export default {
  name: 'Home',
  data(){
    return {
      from_name: '',
      email: '',
      message: ''
    };
  },
  methods: {
    sendEmail() {
      emailjs.sendForm(process.env.VUE_APP_SERVICE_ID, process.env.VUE_APP_TEMPLATE_ID, this.$refs.form,
        'mFLhGuCR5gY8A0Ry9', {
          to_name: 'Nicolas Walcker'
        }).then((response)=>{
          console.log(response.status, response.text);
        }).catch((err)=>{
          console.log(err.status, err.text);
        });

      // Reset form field
      this.from_name = '';
      this.email = '';
      this.message = '';
    },
  }
};
</script>

<style scoped>
* {box-sizing: border-box;}

.container {
  display: block;
  margin:auto;
  text-align: center;
  border-radius: 5px;
  background-color: #f2f2f2;
  padding: 20px;
  width: 50%;
}

label {
  float: left;
}

input[type=text], [type=email], textarea {
  width: 100%;
  padding: 12px;
  border: 1px solid #ccc;
  border-radius: 4px;
  box-sizing: border-box;
  margin-top: 6px;
  margin-bottom: 16px;
  resize: vertical;
}

input[type=submit] {
  background-color: #4CAF50;
  color: white;
  padding: 12px 20px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

input[type=submit]:hover {
  background-color: #45a049;
}
</style>