<template>
  <div class="message">
    <ul v-for="(message, index) in shownMessages" v-bind:key="index">
      <li>
        <h5>{{ message.title }}</h5>
        <p>{{ message.text }}</p>
      </li>
    </ul>
    <p v-if="hidenMessagesCount > 0">
      {{ hidenMessagesText() }}
    </p>
  </div>
</template>

<script>
import { mapGetters} from "vuex";
export default {
  data() {
    return {
      maxShowCount: 3,
    };
  },
  computed: {
    ...mapGetters(["messageCount", "messages"]),
    shownMessages() {
      if (this.messageCount < this.maxShowCount) return this.messages;
      else return this.messages.slice(0, this.maxShowCount);
    },
    hidenMessagesCount() {
      return Math.max(0, this.messageCount - this.maxShowCount);
    },
  },
  methods: {
    hidenMessagesText() {
      if (this.hidenMessagesCount < 5)
        return `Ще ${this.hidenMessagesCount} повідомленя`;
      else return `Ще ${this.hidenMessagesCount} повідомлень`;
    },
  },
};
</script>
