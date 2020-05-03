<template>
  <q-page padding>
    <div class="row">
      <div class="col row notification noNotification" v-if="notificationsInDay == 0">
        <p class="col-4 iconNotification">
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
      <div class="col notification pendingNotification" v-else>
        <div class="row" style="margin-bottom: 5px">
          <p class="col-4 iconNotification">
            <img src="../statics/sadplant.png">
          </p>
          <div class="col-8">
            <p class="titleNotification">Deu ruim!</p>
            <p class="captionNotification">
              Você tem algumas notificações pendentes. Confira:
            </p>
          </div>
        </div>
        <div class="row"
          v-for="notification in this.allNotificationsDay()"
          :key="notification.id"
          v-bind="notification">
          <NextAction class="currentNotifications"
            v-bind="notification"
          >
          </NextAction>
        </div>
      </div>
    </div>
  <div>
  </div>
    <q-card>
      <q-card-section class="row">
        <div class="col-12 text-h6">Proximas ações:</div>
        <div class="cardsNextAction">
          <NextAction
            v-for="notification in this.nextAction()"
            :key="notification.id"
            v-bind="notification"
          />
          <div style="margin: 0px; padding: 0px" v-if="this.nextAction().length == 0">
            <p style="margin-top: 10px; margin-bottom: 5px">
              Você não possui nenhum lembrete cadastrado.
            </p>
            <p>
              Deseja <a href="#">cadastrar um</a>?
            </p>
          </div>
        </div>
      </q-card-section>
    </q-card>
    <!-- <button @click="setNotificationsLS()">teste</button> -->
  </q-page>
</template>

<script>
import NextAction from 'components/NextAction'
// eslint-disable-next-line import/no-webpack-loader-syntax
import lembretes from '../assets/lembretes.json'
import { LocalStorage } from 'quasar'

export default {
  components: {
    NextAction,
    // eslint-disable-next-line vue/no-unused-components
    lembretes
  },
  data () {
    // var today = Date.now()
    // console.log(this.allNotificationsDay())
    return {
      notificationsInDay: this.allNotificationsDay().length
    }
  },
  methods: {
    allNotificationsDay () {
      var array = []
      var notifications = this.getNotificationsLS()

      for (var i = 0; i < notifications.length; i++) {
        if (notifications[i].date === '26/05/2020') {
          array.push(notifications[i])
        }
      }

      return array
    },

    nextAction () {
      var array = []
      var notifications = this.getNotificationsLS()
      // var loops = notifications.length < 3 ? notifications.length : 3

      for (var i = 0; i < notifications.length; i++) {
        if (notifications[i].date !== '26/05/2020') {
          array.push(notifications[i])
        }
        if (i === 2) {
          break
        }
      }

      return array
    },

    setNotificationsLS: function (value) {
      var key = 'notification'
      var allValues = this.getNotificationsLS()
      allValues.push(value)
      LocalStorage.set(key, allValues)
    },
    getNotificationsLS: function () {
      var key = 'notification'
      if (!LocalStorage.getItem(key) || LocalStorage.getItem(key) == null) {
        LocalStorage.set(key, [])
      }
      // console.log(LocalStorage.getItem(key))
      return LocalStorage.getItem(key)
    }
  },
  mounted () {
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
  font-size: 20px;
  margin-bottom: 5px;
}
.notification.noNotification .titleNotification{
  color: #20943b;
}
.notification.pendingNotification .titleNotification{
  color: #c10015;
}

.noNotification{
  background-color: #c1f4cd;
  border-color: #21ba45;
}

.pendingNotification{
  background-color: #ffc0c6;
  border-color: #c10015;
}

.currentNotifications{
  background-color: #fde6e8 !important;
}
</style>
