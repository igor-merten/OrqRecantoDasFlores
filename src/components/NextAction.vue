<template>
  <q-card bordered class="col my-card bg-grey-1 q-mt-sm">
    <q-card-section class="col-auto">
      <div class="row items-center no-wrap">
        <div class="col-12">
          <div class="titleCard">{{title}} <span class="dateCard"> - {{date}}</span> </div>
        </div>
      </div>
      <div id="teste" class="captionCard">
        {{caption}}
      </div>
    </q-card-section>

    <q-separator></q-separator>

    <q-card-actions style="padding: 2px 8px" align="right">
      <q-btn flat>Cancelar lembrete</q-btn>
      <!-- <q-btn flat>Ok</q-btn> -->
    </q-card-actions>
  </q-card>
</template>

<script>
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
    }
  },
  mounted () {
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
