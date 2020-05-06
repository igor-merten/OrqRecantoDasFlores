<template>
  <q-card bordered class="col my-card bg-grey-1 q-px-sm q-pb-sm">
    <q-card-section>
      <div class="text-h6">Adicionar Notificação</div>
    </q-card-section>

    <q-card-section>
      <q-form
        @submit="onSubmit"
        class="q-gutter-md"
      >
        <q-input
          filled
          v-model="title"
          type="text"
          label="Titulo *"
          lazy-rules
          :rules="[ val => val && val.length > 0 || 'Por favor, digite o título']"
        />

        <q-input filled
          v-model="date"
          style="padding-bottom: 0px; margin-top: 0px"
          mask="##/##/####"
          label="Data *"
          lazy-rules
          :rules="[checkDate]"
        >
          <template v-slot:append>
            <q-icon name="event">
              <q-popup-proxy ref="qDateProxy" transition-show="scale" transition-hide="scale">
                <q-date v-model="date" mask="DD/MM/YYYY" subtitle="Data" @input="() => $refs.qDateProxy.hide()" />
              </q-popup-proxy>
            </q-icon>
          </template>
        </q-input>

        <q-select filled v-model="frequency" :options="options" label="Frequência">
        </q-select>

        <q-input
          filled
          v-model="caption"
          type="text"
          label="Legenda"
        />

        <div>
          <q-btn label="Cadastrar" class="btnSubmit" type="submit" color="primary"/>
          <q-btn label="Cancelar" @click="cancel()" type="reset" flat class="q-ml-sm btnCancel" />
        </div>
      </q-form>
    </q-card-section>
  </q-card>
</template>

<script>
import { LocalStorage } from 'quasar'

export default {
  name: 'AddNotification',
  porps: {
    LocalStorage
  },
  data () {
    return {
      options: [
        '', 'Semanalmente', 'Mensalmente'
      ],
      title: '',
      date: '',
      caption: '',
      frequency: null
    }
  },
  methods: {
    cancel () {
      this.$emit('cancelButtonClicked')
    },

    onSubmit () {
      var array = {
        title: this.title,
        caption: this.caption,
        date: this.date
      }
      this.$emit('submited', array)
    },

    getAllNotificationsLS: function () {
      var key = 'notification'
      if (!LocalStorage.getItem(key) || LocalStorage.getItem(key) == null) {
        LocalStorage.set(key, [])
      }
      return LocalStorage.getItem(key)
    },

    checkDate (val) {
      if (
        val.length !== 10 ||
        val.slice(0, 2) > 31 ||
        val.slice(0, 2) <= 0 ||
        val.slice(3, 5) > 12 ||
        val.slice(3, 5) <= 0 ||
        val.slice(6) < 2020) {
        return 'Por favor, digite um data válida.'
      }
      return true
    }
  }
}
</script>

<style>
label{
  padding: 0px
}
.btnSubmit{
  background-color: #064319 !important
}
.btnCancel{
  color: #064319 !important
}
/* fundo header calendario e dia selecionado */
.q-date__header, .q-btn--unelevated{
  background-color: #064319 !important
}
.q-field--focused .q-field__control{
  color: #064319
}
</style>
