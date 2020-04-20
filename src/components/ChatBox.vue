<template>
  <section class="chat-box">
    <div class="chat-nav">
      <img alt="avatar" src="/icons/avatar.svg" class="avatar">
      <button id="helpButton" alt="send messsage" class="help-button"><img alt="send messsage" src="/icons/icon-help.svg"></button>
    </div>
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
      <input type="text" v-model="message" @keyup.enter="sendMessage" @keyup="activeTyping" placeholder="Ask me something...">
      <button @click="sendMessage" class="send-icon">
        <svg width="24px" height="24px" viewBox="0 0 24 24" version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
            <g id="Page-1" stroke="none" stroke-width="1" fill="none" fill-rule="evenodd">
                <g id="icon" transform="translate(-335.000000, -772.000000)" fill="#D8D8D8" fill-rule="nonzero">
                    <path d="M358.243567,772.053744 L335.297794,782.054626 C334.891508,782.248393 334.90401,782.829694 335.316546,783.01096 L341.523343,786.517519 C341.892126,786.723788 342.348416,786.680034 342.667194,786.40501 L354.905773,775.854079 C354.98703,775.785323 355.180797,775.654062 355.255804,775.729068 C355.337061,775.810326 355.21205,775.997842 355.143294,776.079099 L344.55486,788.005151 C344.261084,788.33643 344.217331,788.823973 344.454851,789.199006 L348.511459,795.705829 C348.711477,796.099614 349.280277,796.093364 349.461543,795.693328 L358.949879,772.747556 C359.156147,772.297516 358.687356,771.841226 358.243567,772.053744 Z" id="icon-send"></path>
                </g>
            </g>
        </svg>
      </button>
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
    activeTyping(){

      const sendIcon = document.querySelector(".send-icon svg #icon");

      if (this.message != '') {
        sendIcon.style.fill = "#118CCF";
      } else {
        sendIcon.style.fill = "#D8D8D8";
      }

    },
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
.chat-nav
.message-container{
  height: calc(100vh - 113px);
  max-height: 568px;
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
  opacity: .6;
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
  caret-color: #118CCF;
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
  padding-right: 0;
}

</style>
