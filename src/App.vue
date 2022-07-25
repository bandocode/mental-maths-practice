<template>
  <div class="container">
    <AnswerArea/>
  </div>
</template>

<script>

import AnswerArea from './components/AnswerArea'

export default {
  name: 'App',
  components: {
    AnswerArea,
}
}
</script>

<style>

@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@400;500;600&display=swap');

* {
  margin:0;
  padding:0;
}

:root  {
  --highlight: #818384;
  --bg-colour:  #1e1f1d;
  --font-colour: white;
}


body {
  background-color: var(--bg-colour);
}

.container {
  display: flex;
  height: 100vh;
  width: 100vw;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  position: relative;

}


</style>
