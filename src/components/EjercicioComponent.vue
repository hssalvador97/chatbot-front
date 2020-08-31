<template>
    <div class="container">
  <header class="text-center">
    <h2 class="display-4 text-white">Ejercicio 1</h2>
  </header>

  <div>

<div class="row center-content">
    <input type="text" v-model="cadena"  placeholder="(Hola (mundo)">
    <button v-on:click="modificar">Enviar</button>
</div>

<div class="row center-content">
<ul class="bordes">
    <li v-for="item of list" :key="item">
        {{item}}
    </li>
</ul> 
</div>

  </div>
    </div>
</template>
<script>
export default {
    name:'ChatComponent', 
       data: function()
    {
        return {
            cadena:"",
            words:null,
            elements:[], 
            lengthElements:0, 
            characters:[],
            AuxCharacters:[],  
            list:[],
            element:null, 
        }
    }, 
  
    methods:{
    modificar(){
       this.words=null; 
       this.list=[]; 
        this.list.push(this.cadena);
        while(this.words!="")
        {
            this.words="";
            this.elements=this.cadena.split("("); 
            this.lengthElements=this.elements.length;
            this.elements[this.lengthElements-1]=this.elements[this.lengthElements-1].split(")",1).toString();
  
            for(let i=1; i<this.lengthElements; i++)
            {
     
                if(i!=this.lengthElements-1)
                {
                    this.words=this.words+"("+this.elements[i];
                }
            else{
                    this.characters=this.elements[i].split("");
                    this.AuxCharacters=[]; 
                    for(let j=this.characters.length-1; j>=0; j--)
                    {
                        this.AuxCharacters.push(this.characters[j]);
                        this.elements[i]=""; 
                    }
                    this.AuxCharacters.forEach(dato=>
                    {
                        this.elements[i]=this.elements[i]+dato; 
                    }); 
                    this.words=this.words+this.elements[i]; 
                }
            }
            if(this.words!="")
            this.list.push(this.words);
            this.cadena=this.words; 
        }

        }

    }
     

}
</script>

<style>
    .center-content
    {
        padding-top: 80px;
        /* width: 100%; */
        display: flex;
        justify-content: center;
    }
    li
    {
        list-style: none;
        padding: 5px;
        border-radius: 31px 31px 31px 31px;
        -moz-border-radius: 31px 31px 31px 31px;
        -webkit-border-radius: 31px 31px 31px 31px;
        background: #fafafa;
    }
</style>