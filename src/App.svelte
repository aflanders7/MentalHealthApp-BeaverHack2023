<script>
  import Router from 'svelte-spa-router';
  import Home from './Home.svelte';
  import breath from './breath.svelte';
  import about from './about.svelte';
  import reflect from './reflect.svelte';
  import chatbot from './chatbot.svelte';
</script>

<nav class ="main">
  <a href="/#/">Home</a>
  <a href="/#/chatbot">Chat</a>
  <a href="/#/breath">Breath</a>
  <a href="/#/reflect">Reflect</a>
  <a href="/#/about">About</a>
</nav>

<Router routes={{
  '/': Home,
  '/chatbot': chatbot,
  '/breath': breath,
  '/reflect': reflect,
  '/about': about,
}} />


<footer><p>Disclaimer: This website provides information for informational purposes only. This website does not provide any 
  medical or professional advice. This chatbot does not replace a healthcare professional or act as a substitute for 
  professional mental health, mental advice, diagnosis or treatment.</p>
  &copy; 2023 Audrey Flanders and Lorenzo Balderrama
</footer>