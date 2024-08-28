<template>
    <div class="register-container">
      <h2>Cadastro de Usuário</h2>
      <form @submit.prevent="handleSubmit">
        <div class="form-group">
          <label for="fullName">Nome Completo</label>
          <input
            type="text"
            id="fullName"
            v-model="form.fullName"
            required
          />
        </div>
        <div class="form-group">
          <label for="institution">Instituição de Ensino</label>
          <input
            type="text"
            id="institution"
            v-model="form.institution"
            required
          />
        </div>
        <div class="form-group">
          <label for="cep">CEP</label>
          <input
            type="text"
            id="cep"
            v-model="form.cep"
            @blur="fetchLocation"
            required
          />
        </div>
        <div class="form-group">
          <label for="email">Email</label>
          <input
            type="email"
            id="email"
            v-model="form.email"
            required
          />
          <span v-if="emailError" class="error-message">{{ emailError }}</span>
        </div>
        <div class="form-group">
          <label for="confirmEmail">Confirmar Email</label>
          <input
            type="email"
            id="confirmEmail"
            v-model="form.confirmEmail"
            required
          />
          <span v-if="emailMismatch" class="error-message">Emails não conferem</span>
        </div>
        <div class="form-group">
          <label for="password">Senha</label>
          <input
            type="password"
            id="password"
            v-model="form.password"
            required
            minlength="8"
          />
        </div>
        <div class="form-group">
          <label for="confirmPassword">Confirmar Senha</label>
          <input
            type="password"
            id="confirmPassword"
            v-model="form.confirmPassword"
            required
          />
          <span v-if="passwordMismatch" class="error-message">Senhas não conferem</span>
        </div>
        <button type="submit">Cadastrar</button>
      </form>
      <p>Já tem uma conta? <router-link to="/login">Faça login</router-link></p>
    </div>
  </template>
  
  <script setup>
  import { ref } from 'vue';
  import { useRouter } from 'vue-router';
  
  const form = ref({
    fullName: '',
    institution: '',
    cep: '',
    email: '',
    confirmEmail: '',
    password: '',
    confirmPassword: '',
  });
  
  const emailError = ref('');
  const emailMismatch = ref(false);
  const passwordMismatch = ref(false);
  
  const router = useRouter();
  
  function fetchLocation() {
    // Implemente a lógica para buscar dados de localização a partir do CEP
  }
  
  function handleSubmit() {
    emailError.value = '';
    emailMismatch.value = false;
    passwordMismatch.value = false;
  
    if (form.value.email !== form.value.confirmEmail) {
      emailMismatch.value = true;
      return;
    }
  
    if (form.value.password !== form.value.confirmPassword) {
      passwordMismatch.value = true;
      return;
    }
  
    if (!validateEmail(form.value.email)) {
      emailError.value = 'Email inválido';
      return;
    }
  
    // Adicione aqui o código para enviar os dados do formulário para o backend
    console.log('Formulário enviado:', form.value);
  
    // Após o envio, redirecionar para a página de login
    router.push('/login');
  }
  
  function validateEmail(email) {
    return /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(email);
  }
  </script>
  
  
  <style scoped>
  /* Reset básico */
  body, html {
    margin: 0;
    padding: 0;
    width: 100%;
    height: 100%;
    font-family: Arial, sans-serif;
  }
  
  /* Container de login */
  .login-container {
    display: flex;
    height: 100vh;
  }
  
  /* Lado esquerdo - Imagem com gradiente */
  .left-side {
    flex: 1;
    background: linear-gradient(to bottom, #0575E6, #02298A, #021B79);
    display: flex;
    justify-content: center;
    align-items: center;
    position: relative;
  }
  
  /* Lado direito - Formulário de login */
  .right-side {
    flex: 2;
    background-color: white;
    display: flex;
    justify-content: center;
    align-items: center;
  }
  
  /* Caixa de login */
  .login-box {
    width: 85%;
    max-width: 400px;
    padding: 40px;
    border-radius: 10px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
    background-color: #fff;
  }
  
  /* Estilo do título */
  .login-box h2 {
    margin-bottom: 20px;
    text-align: center;
    color: blue;
  }
  
  /* Estilo dos inputs */
  .login-box input {
    width: 100%;
    padding: 10px;
    margin-bottom: 10px;
    border: 1px solid #ccc;
    border-radius: 15px;
    box-sizing: border-box;
  }
  
  /* Botão de login */
  .login-box button {
    width: 100%;
    padding: 11px;
    background-color: rgb(8, 91, 143);
    color: white;
    border: none;
    border-radius: 10px;
    cursor: pointer;
    transition: background-color 0.3s ease;
  }
  
  /* Efeito de hover no botão */
  .login-box button:hover {
    background-color: rgb(11, 55, 135);
  }
  
  /* Estilo do link "Crie uma" */
  .login-box .btn-link {
    color: rgb(8, 91, 143);
    text-decoration: none;
  }
  
  .login-box .btn-link:hover {
    text-decoration: underline;
  }
  
  /* Imagem no canto */
  .corner-img {
    position: absolute;
    bottom: 0;
    left: 0;
    width: 750px;
    height: auto;
  }
  
  /* Responsividade adicional */
  @media (max-width: 768px) {
    .login-container {
      flex-direction: column;
    }
  
    .left-side {
      display: none;
    }
  
    .right-side {
      flex: 1;
    }
  
    .corner-img {
      display: none;
    }
  }
  
  /* Adiciona o container das bolhas e define a posição */
  .bubbles {
    position: absolute;
    top: 0;
    right: 0;
    width: 100%;
    height: 100%;
    pointer-events: none;
    overflow: hidden;
  }
  
  /* Define o estilo das bolhas */
  .bubble {
    position: absolute;
    width: 50px;
    height: 50px;
    background-color: rgba(0, 123, 255, 0.153);
    border-radius: 50%;
    animation: float 10s infinite;
    opacity: 0;
  }
  
  /* Animação das bolhas */
  @keyframes float {
    0% {
      transform: translateY(100vh) scale(0);
      opacity: 0;
    }
    50% {
      transform: translateY(-50vh) scale(1);
      opacity: 1;
    }
    100% {
      transform: translateY(-100vh) scale(0);
      opacity: 0;
    }
  }
  
  /* Posiciona as bolhas em locais aleatórios e diferentes tamanhos dentro do lado direito */
  .bubbles .bubble:nth-child(1) {
    right: 5%;
    animation-duration: 8s;
    animation-delay: 0s;
  }
  .bubbles .bubble:nth-child(2) {
    right: 10%;
    animation-duration: 10s;
    animation-delay: 2s;
  }
  .bubbles .bubble:nth-child(3) {
    right: 15%;
    animation-duration: 12s;
    animation-delay: 4s;
  }
  .bubbles .bubble:nth-child(4) {
    right: 20%;
    animation-duration: 15s;
    animation-delay: 6s;
  }
  .bubbles .bubble:nth-child(5) {
    right: 25%;
    animation-duration: 20s;
    animation-delay: 9s;
  }
  </style>
  