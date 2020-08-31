<template>
    <div class="container">
    <div class="container py-0 px-4">
  <header class="text-center">
    <h2 class="display-4 text-white">Ejercicio 2</h2>
  </header>
<div class="row rowCenter">
  <div class="row rounded-lg overflow-hidden shadow">
    <div class="col-12 px-1">
      <div class="px-4 py-5 chat-box bg-white">
        <div class="media w-50 mb-3" v-for="(item, type) of messages" :key="type">
          
          <img v-if="item.type==0"  src="./../assets/bot.png" alt="user" width="50" class="rounded-circle">
          <div class="media-body ml-3" :class="{'mover1' : item.type==1}">
            <div class=" rounded py-2 px-3 mb-2" :class="{'principal' :item.type==1 ,'secundario': item.type==0}">
              <p class=" mb-0 " :class="{'txt1' :item.type==1 ,'txt2': item.type==0}">{{item.mensaje}}</p>
            </div>
          </div>
        </div>
         
      </div>
        <div class="input-group bg-light">
          <input type="text" placeholder="Ingresa una mensaje" v-model="mensaje" aria-describedby="button-addon2" class="form-control rounded-0 border-0 py-4 bg-light">
          <div class="input-group-append" v-on:click="sendMessage" @keyup.="sendMessage()">
            <button id="button-addon2"    class="btn btn-link">Enviar</button>
          </div>
        </div>
    </div>
  </div>
</div>
</div>
    </div>

</template>

<script>
import io from 'socket.io-client'; 
export default {
    name:'ChatComponent', 
       data: function()
    {
        return {
            username:"",
            socket:io("https://api-rest-chatbot.herokuapp.com"), 
            messages:[], 
            mensaje:"",
            users:[], 

        }
    }, 
  
    methods:{
      sendMessage: function()
      {
          this.socket.emit('message', this.mensaje);
          this.mensaje="";
      },

     listen: function()
     {
      

      this.socket.on('userOnline'), user=>
      {
       this.users.push(user); 
      }

      this.socket.on('mensaje', messege=>
      {

       this.messages.push(messege);
      })
     }

        }, 
        mounted: function()
    {
        this.listen();
    }

}
</script>

<style>
 @import url('https://fonts.googleapis.com/css?family=Montserrat&display=swap');
    * {
        font-family: 'Montserrat', Sans-serif;
    }
    .mover1 {
        position: relative;
        left: 100%;
    }
    
    .txt1 {
        color: white;
    }
    
    .txt2 {
        color: black;
    }
    
    .principal {
        background-color: #007bff;
    }
    
    .secundario {
        background-color: #F2F6F7;
    }
.rowCenter
{
    display: flex;
    justify-content: center;    
}
body {
  background-color: #fafafa;
 background-image: linear-gradient(80deg, #749EA4 0%, #1685A8 100%); 
  min-height: 100vh;
}
::-webkit-scrollbar {
  width: 5px;
}
::-webkit-scrollbar-track {
  width: 5px;
  background: #f5f5f5;
}
::-webkit-scrollbar-thumb {
  width: 1em;
  background-color: #ddd;
  outline: 1px solid slategrey;
  border-radius: 1rem;
}
.text-small {
  font-size: 0.9rem;
}
.messages-box,
.chat-box {
  height: 700px;
  overflow-y: scroll;
}
.rounded-lg {
  border-radius: 0.5rem;
}
input::placeholder {
  font-size: 0.9rem;
  color: #999;
}

</style>