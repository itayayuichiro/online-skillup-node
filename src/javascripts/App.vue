<template>
    <div>
        <nav class="navbar navbar-expand-lg navbar-light bg-light">
            <a class="navbar-brand" href="#">チャットアプリケーション</a>
            <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarSupportedContent"
                    aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
                <span class="navbar-toggler-icon"></span>
            </button>
        </nav>
        <div class="container">
            <p>
                <img class="logo" src="../images/logo.jpg" alt="ロゴ">
            </p>
            <MyComponent :messages="$data.messages" :user_name="this.$data.name"/>
            <form @submit="onSubmit">
                <div class="form-group">
                    <label>お名前</label>
                    <input v-model="$data.name" type="text" class="form-control">
                    <label>メッセージ</label>
                    <input v-model="$data.text" type="text" class="form-control">
                    <br>
                    <button type="submit" class="form-control btn-primary">送信</button>
                </div>
            </form>
        </div>
    </div>
</template>

<script>
import socket from './utils/socket';
// components
import MyComponent from './components/MyComponent.vue';

export default {
  components: {
    MyComponent
  },
  data() {
    return {
      text: '',
      name: '',
      messages: [
      ],
    };
  },
  created() {
    socket.on('connect', () => {
      console.log('connected!');
    });

    socket.on('send', (message, name) => {
      // console.log(message);
      this.$data.messages.push({ 'text': message, 'name': name });
    });
  },
  methods: {
    /**
     * Enterボタンを押したとき
     */
    onSubmit(e) {
      e.preventDefault();
      socket.emit('send', this.$data.text, this.$data.name);
    }
  }
};
</script>

<style lang="scss">
  .logo {
    width: 40px;
  }

  .sample {
    color: $red;
  }

  .mytext {
    border: 0;
    padding: 10px;
    background: whitesmoke;
  }

  .text {
    width: 75%;
    display: flex;
    flex-direction: column;
  }

  .text > p:first-of-type {
    width: 100%;
    margin-top: 0;
    margin-bottom: auto;
    line-height: 13px;
    font-size: 12px;
  }

  .text > p:last-of-type {
    width: 100%;
  }

  .text-l {
    float: left;
    padding-right: 10px;
  }

  .text-r {
    float: right;
    padding-left: 10px;
  }

  .avatar {
    display: flex;
    justify-content: center;
    align-items: center;
    width: 25%;
    float: left;
    padding-right: 10px;
  }

  .macro {
    margin-top: 5px;
    width: 85%;
    border-radius: 5px;
    padding: 5px;
    display: flex;
  }

  .msj-rta {
    float: right;
    background: whitesmoke;
  }

  .msj {
    float: left;
    background: white;
  }

  .frame {
    background: #e0e0de;
    height: 450px;
    overflow: hidden;
    padding: 0;
    max-width: 100%;
  }

  .frame > div:last-of-type {
    position: absolute;
    bottom: 0;
    width: 100%;
    display: flex;
  }

  body > div > div > div:nth-child(2) > span {
    background: whitesmoke;
    padding: 10px;
    font-size: 21px;
    border-radius: 50%;
  }

  body > div > div > div.msj-rta.macro {
    margin: auto;
    margin-left: 1%;
  }

  ul {
    width: 100%;
    list-style-type: none;
    padding: 18px;
    position: absolute;
    bottom: 47px;
    display: flex;
    flex-direction: column;
    top: 0;
    overflow-y: scroll;
  }

  .msj::before {
    width: 0;
    height: 0;
    content: '';
    top: -5px;
    left: -14px;
    position: relative;
    border-style: solid;
    border-width: 0 13px 13px 0;
    border-color: transparent #fff transparent transparent;
  }

  .msj-rta::after {
    width: 0;
    height: 0;
    content: '';
    top: -5px;
    left: 14px;
    position: relative;
    border-style: solid;
    border-width: 13px 13px 0 0;
    border-color: whitesmoke transparent transparent transparent;
  }

  input:focus {
    outline: none;
  }

  ::-webkit-input-placeholder { /* Chrome/Opera/Safari */
    color: #d4d4d4;
  }

  ::-moz-placeholder { /* Firefox 19+ */
    color: #d4d4d4;
  }

  :-ms-input-placeholder { /* IE 10+ */
    color: #d4d4d4;
  }

  :-moz-placeholder { /* Firefox 18- */
    color: #d4d4d4;
  }
</style>
