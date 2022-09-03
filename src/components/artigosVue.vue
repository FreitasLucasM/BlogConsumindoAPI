<template>
    <div class="hello">
      <form class="form">
        <p>
          <input type="text" placeholder="insira o titulo" class="entrada" v-model="artigo.titulo">
        </p>
        <p>
          <textarea class="entrada" placeholder="insira o conteudo" name="conteudo" id="" cols="30" rows="10" v-model="artigo.conteudo"></textarea>
        </p>
        <input type="hidden" v-model="artigo.id">
        <p>
          <button class="sucess" v-on:click="cadastrarArtigos()">Cadastrar</button>
        </p>
      </form>

      <div class="card" >
        <div class="post" v-for="artigo in artigos" v-bind:key="artigo.id" id= artigo.id>
          <h3>{{artigo.titulo}}</h3>
          <p>{{artigo.conteudo}}</p>
          <p>
          <button class="danger" @click="deletarArtigo(artigo.id)">deletar</button>
          <button class="danger" @click="editarArtigo(artigo)">Editar</button>
          </p>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    name: 'artigosVue',
    data(){
      return{
        artigos:[
        ],
        artigo:{
          id:'',
          titulo:'',
          conteudo:''
        }
      }
    },
    methods:{
      fetchArtigos(){
         fetch('http://127.0.0.1:8000/api/artigos')
          .then(data => data.json())
          .then(({data}) => this.artigos = data)
      },
      cadastrarArtigos(){
        if(this.artigo.titulo == ''){
          alert('preencha todos os campos')
          return
        }
        if(this.artigo.conteudo == ''){
          alert('preencha todos os campos')
          return
        }
        //alert('artigo é ' +this.artigo.titulo + '\nconteudo:' +this.artigo.conteudo)
        fetch('http://127.0.0.1:8000/api/artigo', {
          method: 'post',
          body: JSON.stringify(this.artigo),
          headers:{
            'Content-Type':'application/json'
          }
        })
        .then(res=>res.json()).catch(err=>console.warn(err))
        alert('Dados inseridos com sucesso!')
        this.fetchArtigos()
        this.cleanArtigo()
      },
      cleanArtigo(){
        this.artigo.id = '',
        this.artigo.titulo = '',
        this.artigo.conteudo = ''
      },
      deletarArtigo(id){
        fetch('http://127.0.0.1:8000/api/artigo/' + id, {
          method:'delete'
        })
        .then(res=>res.json())
        .catch(err=>console.warn(err))
        .finally(()=>this.fetchArtigos())
      },
      editarArtigo(artigo){

      }
    },
    created(){
      this.fetchArtigos()
    }
  }
  </script>
  
  <!-- Add "scoped" attribute to limit CSS to this component only -->
  <style scoped>
    .hello{
      color: #333;
      padding: 20px;
      max-width: 1200px;
      margin: auto;
    }
  .card{
    background-color: #FFF;
    color: #333;
  }
  .post{
    border: 1px solid silver;
    padding: 10px;
    margin-top: 10px;
    text-align: left;
  }
  h3{
    border-bottom: 1px dotted silver;
    margin-bottom: 10px;
  }
  .disabled{
    text-decoration: none;
    color: #ccc;
    cursor: default;
    pointer-events: none;
  }
  i {color:#333}
  .danger{
    color: #fff;
    background:red;
    padding: 5px;
  }
  .sucess{
    color:#fff;
    background: green;
    padding: 15px;
    border: 1px solid #234700;
  }
  .entrada{
    width: 98%;
    border: 1px solid #000;
    margin-top: 10px;
    padding: 10px;
    font-size: 18px;
    font-weight: bold;
  }
  input.area{height: 30px;}
  textarea.entrada{
    height: 80px;
    margin-bottom: 10px;
  }
    
  </style>
  