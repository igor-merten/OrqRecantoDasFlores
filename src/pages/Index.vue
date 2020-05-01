<template>
  <q-page padding>
    <div class="row">
      <div class="col row notification noNotification" v-if="notificationsInDay == 0">
        <p class="col-4 iconNotification">
          <!-- <q-icon class="iconNotification" name="sentiment_satisfied_alt" /> -->
          <img src="../statics/flower.png">
        </p>
        <div class="col-8">
          <p class="titleNotification">Parabéns!</p>
          <p class="captionNotification">
            Você está seguindo as recomendações de cuidado de forma exemplar! Suas plantas agradecem.
            <q-icon name="eco"></q-icon>
          </p>
        </div>
      </div>
    </div>

  <q-card>
    <q-card-section class="row">
      <div class="col-12 text-h6">Proximas ações:</div>
      <div class="row cardsNextAction">
        <NextAction
            v-for="notification in notifications"
            :key="notification.id"
            v-bind="notification"
          />
        </div>
    </q-card-section>
  </q-card>

    <!-- <div class="row">
      <p class="col">Proximas ações:</p>
    </div>
    <div class="row">
        <q-list class="col" bordered separator>
        <NextAction
          v-for="notification in notifications"
          :key="notification.id"
          v-bind="notification"
        />
        </q-list>
      </div> -->
    <!-- <button
      style="position: absolute; right: 10px;"
      @click="counter++"
    >
      {{counter}}
    </button>

    <div class="q-pa-md q-gutter-sm">
      <q-avatar
        v-for="size in ['xs', 'sm', 'md', 'lg', 'xl']"
        :key="size"
        :size="size"
        color="primary"
        text-color="white"
        icon="directions"
      />
    </div>

    <input
      v-model="message"
      type="text"
      @keyup.esc="clearMessage"
      @keyup.enter="alertMessage"
      v-autofocus
      :style="errorStyle"
      ref="messageInput"
      >
      @mouseenter="alertMessage"
    <button @click="clearMessage">Clear</button>
    <h5
      v-if="message.length"
      class="border-grey">{{ message }}</h5>
    <h6 v-else>No message entered</h6>

    <hr>

    <p>Uppercase message: {{ messageUppercase }}</p>
    <p>Lowercase message: {{ message | messageLowercase }}</p> -->
  </q-page>
</template>

<script>
import NextAction from 'components/NextAction'

export default {
  components: {
    NextAction
  },
  data () {
    return {
      notificationsInDay: 0,
      notifications: [
        {
          id: 1,
          title: 'Rega',
          caption: 'Você precisa molhar as plantas. porque elas podem morrer e esse texto ficou bem grande',
          date: '13/05/2020'
        },
        {
          id: 2,
          title: 'Adubação',
          caption: 'É preciso adubar as Cattleyas com Basacote.',
          date: '20/05/2020'
        },
        {
          id: 3,
          title: 'Enraizar mudas',
          caption: 'É preciso enraizar os dendrobiuns com Superdrive.',
          date: '26/05/2020'
        }
      ]
    }
  },
  // computed: {
  //   messageUppercase () {
  //     console.log('Message Uppercase was fired.')
  //     return this.message.toUpperCase()
  //   },
  //   errorStyle () {
  //     if (this.message.length > 22) {
  //       return {
  //         color: 'red', background: 'pink'
  //       }
  //     }
  //     return null
  //   }
  // },
  // methods: {
  //   clearMessage () {
  //     console.log('a')
  //     this.message = ''
  //   },
  //   handleKeyup (e) {
  //     console.log(e)
  //     if (e.keyCode === 32) {
  //       this.clearMessage()
  //     } else if (e.keyCode === 13) {
  //       this.alertMessage()
  //     }
  //   },
  //   alertMessage () {
  //     alert(this.message)
  //   }
  // },
  // filters: {
  //   messageLowercase (value) {
  //     return value.toLowerCase()
  //   }
  // },
  // directives: {
  //   autofocus: {
  //     inserted (el) {
  //       el.focus()
  //     }
  //   }
  // },
  mounted () {
    // this.$refs.messageInput.className = 'bg-green'
  }
}
</script>

<style>
.notification{
  margin: 10px 0px;
  border-radius: 4px;
  padding: 16px 24px;
  border-width: 0px 2px;
  border-style: solid;
}

.notification .iconNotification{
  text-align: center;
  margin: 0px;
  padding-right: 31px;
  padding-top: 15px;
}
.notification .iconNotification img{
  margin: 0px auto;
  width: auto;
  max-height: 60px;
}
.notification .captionNotification{
  text-align: justify;
  margin: 0px
}
.notification .titleNotification{
  font-weight: bold;
  color: #20943b;
  font-size: 20px;
  margin-bottom: 5px;
}

.noNotification{
  background-color: #c1f4cd;
  border-color: #21ba45;
}

/* .border-grey{
  border: 1px solid grey;
}
input, button {
  font-size: 23px;
}
.error{
  color: red;
  background: pink;
} */

</style>
