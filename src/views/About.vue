<template>
  <div class="about">
    <h1>Text: {{ text.messege }}</h1>
  </div>
</template>

<script>
export default {
  data() {
    return {
      text: '',
    };
  },
  beforeMount() {
    fetch('http://localhost:3030/content', {
      headers: {
        authorization: `Bearer ${localStorage.getItem('token')}`,
      },
    })
      .then((res) => res.json())
      .then((data) => {
        this.text = data;
      });
  },
};
</script>
