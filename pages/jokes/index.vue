<template>
    <div>
        <search-jokes v-on:search-text="searchText"></search-jokes>
        <Joke v-for="joke in jokes" :key="joke.id" :id="joke.id" :joke="joke.joke" />
    </div>
</template>
<script>
export default {
    data() {
        return {
            jokes: []
        }
    },
    async created() {
        const config = {
            headers: {
                'Accept': 'application/json'
            }
        }

        try {
            const res = await this.$axios.$get('https://icanhazdadjoke.com/search', config);
            this.jokes = res.results
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
    },
    methods: {
        async searchText(text) {
            const config = {
                headers: {
                    'Accept': 'application/json'
                }
            }

            try {
                const res = await this.$axios.$get(`https://icanhazdadjoke.com/search?term=${text}`, config);
                this.jokes = res.results
            } catch (error) {
                console.log('error', error);
            }
        }
    },

}
</script>