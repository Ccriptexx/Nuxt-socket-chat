<template>
  <v-text-field
    label="Ввудите сообщение"
    variant="outlined"
    v-model="text"
    @keydown.enter="send"
  />
</template>

<script>
export default {
  data: () => ({
    text: ''
  }),
  methods: {
    send() {
      this.$socket.emit('createMessage', {
        text: this.text,
        id: this.$store.state.user.id
      }, data => {
        if (typeof data === 'string') {
          console.error(data)
        } else {
          this.text = ''
        }
      })
    }
  }
}
</script>
