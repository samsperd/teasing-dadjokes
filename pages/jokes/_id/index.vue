<template>
    <div>
        <nuxt-link to="/jokes">
            Back To Jokes
        </nuxt-link>
        <h2>
            {{ joke }}
        </h2>
        <hr>
        <small> Joke ID: {{ $route.params.id }} </small>
    </div>
</template>
<script>
export default {
    data() {
        return {
            joke: {}
        }
    },
    async created() {
        const config = {
            headers: {
                'Accept': 'application/json'
            }
        }

        try {
            const res = await this.$axios.$get(`https://icanhazdadjoke.com/j/${this.$route.params.id}`, config);
            this.joke = res.joke
        } catch (error) {
            console.log('error', error);
        }
    },
    head() {
        return {
            title: "Jokes",
            meta: [
                {
                    hid: "description",
                    name: "description",
                    content: "Best place for corny dad jokes"
                }
            ]
        }
  }
}
</script>