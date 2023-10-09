<template>
  <div>
    <v-text-field v-model="textInput" label="Entrez votre texte"></v-text-field>
    <v-btn @click="valider">Valider</v-btn>
  </div>
</template>

<script>
export default {
  data() {
    return {
      textInput: ''
    }
  },
  methods: {
    valider() {
      if (this.textInput.trim() !== '') {
        this.$router.push(`/stats/${encodeURIComponent(this.textInput)}`);
      }
    }
  }
}
</script>