<template>
    <div>
        <h1>Release that!</h1>
        <textarea v-model="rawTicketData" name="name" rows="8" cols="80"></textarea>
        <button type="button" name="button" @click="generateReleaseNotes">Generate</button>

        <div class="results">
            <h3>Result</h3>
            <ul>
                <li v-for="ticket in tickets" v-bind:key="ticket.tron">
                    <a v-bind:href="ticket.href">{{ ticket.tron }}: {{ ticket.name }}</a>
                </li>
            </ul>
        </div>

        <div class="emoji-generator">
            Please supply emoji or slack emoji code:
            <input v-model="emojis" type="text"><br>
            Please supply title of release:

            <input v-model="rawTitle" type="text"><br>
            <button type="button" name="button" @click="generateEmojiTitle">Gimme!</button>

            <h3>Result</h3>
            <p>{{ this.generatedTitle }}</p>
        </div>

    </div>
</template>

<script>
export default {
  name: 'Kraken',
  data () {
      return {
          rawTicketData: '',
          tickets: [],
          emojis: '',
          rawTitle: '',
          generatedTitle: '',
      };
  },
  methods: {
    generateReleaseNotes () {
        // clear tickets
        this.tickets = [];

        this.rawTicketData.split('\n').forEach(ticket => {
            const ticketInfo = parseTicketInformation(ticket);
            this.tickets = [...this.tickets, ticketInfo];
        });

        console.log(this.tickets);

        function parseTicketInformation(text) {
            text = text.split('\t');

            return {
                'tron': text[2],
                'name': text[3],
                'href': generateTicketLink(text[2])
            };
        }

        function generateTicketLink (ticketId) {
            return "https://redbrickmedia.atlassian.net/browse/" + ticketId;
        }
    },
    generateEmojiTitle () {
        this.generatedTitle = `${ this.emojis } ${this.rawTitle} ${ this.emojis.split('').reverse().join('') }`
        console.log(this.generatedTitle);
    }
  },
}

// 🤞🦆💪
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    h1 {
        color: cornflowerblue;
    }

    textarea {
        display: block;
        margin: auto;
        margin-bottom: 1rem;
    }

    button {
        font-family: Avenir, Helvetica, Arial, sans-serif;
        font-weight: bold;
        width: 200px;
        height: 40px;
        border-radius: 5px;
        background: none;
        border: 2px solid black;
        cursor: pointer;
    }

    ul {
        text-align: left;
        list-style-type: none;
    }

    ul li a {
        text-decoration: none;
    }
</style>
