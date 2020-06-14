<template>

  <transition name="fade" mode="out-in">

  <q-form
    @submit.prevent="addNotificationPositionChange(1)"
    class="q-gutter-md"
    v-if="addNotificationPosition === 0"
    key="Titulo"
    >

    <q-card bordered class="col my-card bg-grey-1 q-px-sm q-pb-sm">
      <q-card-section>
        <div class="text-h6">Qual título deve ter a notificação?</div>
      </q-card-section>

      <q-card-section>
          <q-input
            filled
            v-model="title"
            type="text"
            label="Titulo *"
            color="primary"
            lazy-rules
            :rules="[ val => val && val.length > 0 || 'Por favor, digite o título']"
          />
      </q-card-section>

      <div>
        <q-btn label="Cancelar" @click="cancel()" type="reset" color="primary" class="q-ml-sm btnCancel" />
        <q-btn label="Seguinte >" class="btnSubmit" type="submit" flat color="primary"/>
      </div>
    </q-card>
  </q-form>

  <q-form
    @submit.prevent="addNotificationPositionChange(1)"
    class="q-gutter-md"
    v-if="addNotificationPosition === 1"
    key="Data"
    >
    <q-card bordered class="col my-card bg-grey-1 q-px-sm q-pb-sm">
      <q-card-section>
        <div class="text-h6">Quando você quer ser notificado?</div>
      </q-card-section>
        <q-card-section>
            <q-input filled
              v-model="date"
              style="padding-bottom: 0px; margin-top: 0px"
              mask="##/##/####"
              label="Data *"
              color="primary"
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
      </q-card-section>

      <div>
        <q-btn label="< Voltar" @click="addNotificationPositionChange(-1)" type="button" flat color="primary" class="q-ml-sm btnCancel" />
        <q-btn label="Seguinte >" class="btnSubmit" type="submit" flat color="primary"/>
      </div>

    </q-card>
  </q-form>

<q-form
    @submit.prevent="addNotificationPositionChange(1)"
    class="q-gutter-md"
    v-if="addNotificationPosition === 2"
    key="Repetir"
    >
  <q-card bordered class="col my-card bg-grey-1 q-px-sm q-pb-sm">
    <q-card-section>
      <div class="text-h6">Você quer que esse lembrete se repita?</div>
    </q-card-section>

    <q-card-section>
      <div class="row">
        <p class="col vertical-middle fontSize18" style="padding: 11px 0px; margin: 0px">Repetir esse lembrete?</p>
        <span align="right" class="col">
          <q-toggle
            v-model="repetir"
          ></q-toggle>
        </span>
      </div>

      <div style="margin-top: 0px" v-show="repetir">
        <div class="row">
          <p class="col vertical-middle" style="padding: 19px 0px; margin: 0px">
            A cada
          </p>
          <div class="q-mr-sm">
            <q-input
              @keydown="pluralOptions()"
              v-model="qntTimes"
              style="width: 50px"
              type="number"
              mask="#"
              fill-mask="1"
              filled
              reverse-fill-mask
              input-class="text-center"
            />
          </div>
          <div class="col">
            <q-select
              v-model="frequency"
              filled
              :options="options"
              emit-value
              map-options
              option-value="options.id"
            />
          </div>
        </div>
        <div>
          <div class="row">
            <p class="col vertical-middle fontSize18" style="padding: 11px 0px; margin: 0px">
              Terminar?
            </p>
            <span align="right" class="col">
              <q-toggle
                v-model="terminar"
              ></q-toggle>
            </span>
          </div>
          <div class="row gutter" v-show="terminar">
            <p class="col vertical-middle" style="padding: 19px 0px; margin: 0px">
              Terminar em
            </p>
            <div class="q-mr-sm">
              <q-input
                v-model="qntTimes"
                style="width: 50px"
                type="number"
                mask="#"
                fill-mask="1"
                filled
                reverse-fill-mask
                input-class="text-center"
              />
            </div>
            <div class="col">
              <q-select v-model="frequency" filled :options="options" />
            </div>
          </div>
        </div>
      </div>
    </q-card-section>

    <div>
      <q-btn label="< Voltar" @click="addNotificationPositionChange(-1)" type="button" flat color="primary" class="q-ml-sm btnCancel" />
      <q-btn label="Seguinte >" class="btnSubmit" type="button" @click="addNotificationPositionChange(1)" flat color="primary"/>
    </div>

  </q-card>
</q-form>

  <q-form
    @submit.prevent="onSubmit"
    class="q-gutter-md"
    v-if="addNotificationPosition === 3"
    key="Legenda"
    >
  <q-card bordered class="col my-card bg-grey-1 q-px-sm q-pb-sm">
    <q-card-section>
      <div class="text-h6">Deseja colocar alguma legenda na notificação?</div>
    </q-card-section>

    <q-card-section>
      <q-input
        filled
        v-model="caption"
        type="text"
        label="Legenda"
        color="primary"
      />

      <div>
        <q-btn label="< Voltar" @click="addNotificationPositionChange(-1)" type="button" flat color="primary" class="q-ml-sm btnCancel" />
        <q-btn label="Cadastrar" class="btnSubmit" type="submit" color="primary"/>
      </div>
    </q-card-section>
  </q-card>
  </q-form>
  </transition>
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
      addNotificationPosition: 0,
      title: '',
      date: '',
      caption: '',
      qntTimes: 1,
      options: [
        { id: 0, value: 'dia' },
        { id: 1, value: 'semana' },
        { id: 2, value: 'mês' },
        { id: 3, value: 'ano' }
      ],
      frequency: 'dia',
      repetir: false,
      terminar: false
    }
  },
  methods: {
    addNotificationPositionChange: function (value) {
      this.addNotificationPosition += value
      if (this.addNotificationPosition < 0 || this.addNotificationPosition > 3) {
        this.addNotificationPosition = 0
      }
      switch (this.addNotificationPosition) {
        case 0: return 'Titulo'
        case 1: return 'Data'
        case 2: return 'Repetir'
        case 3: return 'Legenda'
        default: return 'Titulo'
      }
    },
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
        return 'Por favor, digite uma data válida.'
      }
      return true
    },

    pluralOptions () {
      console.log(this.qntTimes)
      this.options = this.qntTimes === '1' ? ['dia', 'semana', 'mês', 'ano'] : ['dias', 'semanas', 'meses', 'anos']
      console.log(this.options[0])
    }
  }
}
</script>

<style>
label{
  padding: 0px
}
/* .btnSubmit{
  background-color: #064319 !important
}
.btnCancel{
  color: #064319 !important
}
/* fundo header calendario e dia selecionado
.q-date__header, .q-btn--unelevated{
  background-color: #064319 !important
}
.q-field--focused .q-field__control{
  color: #064319
} */
.fontSize18{
  font-size: 18;
}
.fade-enter-active, .fade-leave-active {
  transition: opacity .3s;
}
.fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
  opacity: 0;
}
</style>
