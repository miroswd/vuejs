







<script setup>

  import {ref, reactive, onMounted} from 'vue'; 


  const email = ref(""); // o que for digitado no input, será capturado em tempo real nessa constante
  const password = ref("");

  /**
   * ref - tipos primitivos
   * 
   *  dep: Set(0) {w: 0, n: 0, size: 0}
      __v_isRef: true
      __v_isShallow: false
      _rawValue: "teste"
      _value: "teste"
   */

   const user = reactive({
      email: '',
      password: ''
    });  

   /**
    * reactive - para trabalhar com objetos
    *
    * Proxy {email: 'teste', password: 'pass'}
    */

  const login = () => {
    // console.log(email.value, password.value)
    console.log(user.email, user.password)
  };


  const names = reactive([]) // declarando names q será populado no onmounted

  onMounted(() => {
    // quando quiser fazer algo quando o componente é carregado
    console.log("componente montado");

    names.push(
      { firstName: "Miro", age: 22 },
      { firstName: "John", age: 78 },
      { firstName: "Xuxa", age: 15 },
    );


    // sempre quando faz uma requisição pra uma api, coloca dentro do onMounted
  }); 


  function remove(user) {
    const index = names.findIndex(name => user.firstName === name.firstName);

    names.splice(index,1);
    
  }


</script>


<template>

  <h1 class="text-blue-900 font-bold text-3xl">
    Login
  </h1>

  <template v-if="names.length > 0">
    <ul>
      <li v-for="name in names">
        {{ name.firstName }} - <button v-on:click="remove(name)">Remove</button>
      </li> 
      <!-- V-for no li, pq o q eu quero q repita é o li -->
    </ul>
  </template>


  <template v-else>
    Nenhum user encontrado
  </template>


    {{ email }}
    {{ user.password }}

    <template v-if="user.email.length <=0">
      E-mail vazio
    </template>
    <template v-else>
      E-mail: {{ user.email }}
    </template>


    <form action="" @submit.prevent="login">
      <!-- 
        v-model -> liga o input a um valor
       -->
      <!-- <input type="text" placeholder="Email" v-model="email"> 
      <input type="password" placeholder="Password" v-model="password"> -->
      <input type="text" placeholder="Email" v-model="user.email"> 
      <input type="password" placeholder="Password" v-model="user.password">
      <button type="submit">Login</button>

    </form>

</template>


<style>

</style>