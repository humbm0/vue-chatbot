<template>
  <section class="chat-box">
    <div class="message-container" ref="chatbox">
      <ul>
        <li class="message" v-for="(message, idx) in messages" :key="idx" :class="message.author">
          <div>
            <p>{{ message.text }}</p>
            <span class="time-stamp">{{ message.time }}</span>
            </div>
        </li>
      </ul>
    </div>
    <div class="input-container">
      <input type="text" v-model="message" @keyup.enter="sendMessage" placeholder="Ask me something...">
      <button @click="sendMessage">Send</button>
    </div>
  </section>
</template>

<script>
export default {
  name: 'ChatBox',
  data: () => ({
    message: '',
    messages: []
  }),
  methods: {
    sendMessage() {

      // Check user message isn't empty
      if (this.message != ''){

        var today = new Date();
        var time = today.getHours() + ":" + today.getMinutes();

        // Add user inout to messages list
        this.messages.push({
          text: this.message,
          author: 'user',
          time: time
        })

        // Send user input to API
        // this.axios.get('')
        // .then(res => {
        //   this.messages.push({
        //     text: res.data.output,
        //     author: 'bot'
        //   })
        // })
        
        // Reset user input
        this.message = "";

        // Scroll to latest message
        this.$nextTick(() => {
          this.$refs.chatbox.scrollTop = this.$refs.chatbox.scrollHeight
        })

      }
      
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.chat-box{
  max-width: 539px;
  margin: auto;
  background: #fff;
}
.message-container{
  height: 568px;
  display: flex;
  flex-direction: column;
  list-style-type: none;
  padding: 24px;
  overflow-y: auto;
}

.message div{
  max-width: 100%;
  text-align: right;
  margin-bottom: 16px;
}

.message p{
  padding: 8px 16px 8px 16px;
  text-align: right;
  overflow-wrap: break-word;
  max-width: 83.33333333%;
  margin: 0;
  margin-bottom: 8px;
}


.message.bot div{
  float: left;
  clear: left;
}
.message.bot p{
  background: #f1f1f1;
  border-radius: 16px 16px 16px 4px;
  padding: 8px 16px 8px 16px;
  float: left;
}


.message.user div{
  float: right;
  clear: right;
}
.message.user p{
  background-image: linear-gradient(-45deg,#293189,#0b82c9);
  border-radius: 16px 16px 4px 16px;
  color: #fff;
  float: right;
}

.time-stamp{
  font-size: 14px;
  display: block;
}

.input-container{
  width: 100%;
  border-top: 1px solid #d8d8d8;
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-align: center;
  -ms-flex-align: center;
  align-items: center;
  padding-left: 24px;
  padding-right: 24px;
  box-sizing: border-box;
}
input{
  width: 100%;
  height: 24px;
  border: none;
  font-size: inherit;
}
input:focus{
  outline: none;
}
button{
  width: 48px;
  height: 64px;
  background: none;
  border: none;
  font-size: inherit;
}

</style>
