<template>
  <q-card bordered class="full-width my-card bg-grey-1 q-mt-sm">
    <q-card-section class="col-12">
      <div class="row col-12 items-center no-wrap">
        <div class="col-12">
          <div class="titleCard">{{title}} <span class="dateCard"> - {{date}}</span> </div>
        </div>
      </div>
      <div class="captionCard full-width">
        {{caption}}
      </div>
    </q-card-section>

    <q-separator></q-separator>

    <q-card-actions style="padding: 2px 8px" align="right">
      <q-btn flat @click="remove()"><q-icon style="color: #064319" :name="actionBtnIcon" v-if="actionBtnIcon" /> {{actionBtn}}</q-btn>
      <!-- <q-btn flat>Ok</q-btn> -->
    </q-card-actions>
  </q-card>
</template>

<script>
import { LocalStorage } from 'quasar'

export default {
  name: 'NextAction',
  props: {
    id: {
      type: Number,
      required: true
    },

    title: {
      type: String,
      required: true
    },

    caption: {
      type: String,
      default: ''
    },

    date: {
      type: String,
      default: ''
    },
    actionBtn: String,
    actionBtnIcon: String
  },
  methods: {
    remove: function () {
      var key = 'notification'
      var notifications = LocalStorage.getItem(key)
      var index
      var id = this.id
      notifications.find(function (item, i) {
        if (item.id === id) {
          index = i
        }
      })
      notifications.splice(index, 1)
      LocalStorage.set(key, notifications)
      location.reload()
    }
  }
}
</script>

<style>
  .my-card{
    text-align: justify;
  }
  .titleCard{
    font-size: 14px;
    font-weight: bold;
  }
  .dateCard{
    font-size: 12px;
    font-weight: normal;
  }
  .captionCard{
    margin-top: 5px;
  }
</style>
