<template>
  <q-card bordered class="col my-card bg-grey-1" style="position:relative; padding-bottom: 58px">
    <q-card-section class="col-auto">
      <div class="row items-center no-wrap">
        <div class="col-12">
          <div class="titleCard">{{title}}</div>
          <div class="dateCard">{{date}}</div>
        </div>
      </div>
      <div id="teste" class="captionCard">
        {{caption}}
      </div>

          <!-- <div class="col-auto">
            <q-btn color="grey-7" round flat icon="more_vert">
              <q-menu cover auto-close>
                <q-list>
                  <q-item clickable>
                    <q-item-section>Remove Card</q-item-section>
                  </q-item>
                  <q-item clickable>
                    <q-item-section>Send Feedback</q-item-section>
                  </q-item>
                  <q-item clickable>
                    <q-item-section>Share</q-item-section>
                  </q-item>
                </q-list>
              </q-menu>
            </q-btn>
          </div>
        </div> -->
    </q-card-section>

    <q-card-actions class="col-auto" style="position: absolute; bottom: 0px; display: inline-block;">
      <q-separator style="height: 1px; margin-bottom: 8px"></q-separator>
      <q-btn flat>Cancelar lembrete</q-btn>
      <!-- <q-btn flat>Ok</q-btn> -->
    </q-card-actions>
  </q-card>
  <!-- <q-item
    clickable
    v-ripple
  >
    <q-item-section>
      <q-item-label>{{ this.title }}</q-item-label>
      <q-item-label caption>
        {{ caption }}
      </q-item-label>
      <q-item-label caption>
        Em: <span class="text-weight-bold">{{ date }}</span>
      </q-item-label>
    </q-item-section>
  </q-item> -->
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

    // icon: {
    //   type: String,
    //   default: ''
    // }
  },
  mounted () {
    document.getElementsByClassName('captionCard').classList.add('full-height')
    // document.getElementById('teste').classList.add('full-height')
  }
}
</script>

<style>
  .my-card{
    /* margin-right: 2px; */
    width: 32.3%;
    margin-right: 1%;
  }
  .titleCard{
    font-size: 14px;
    font-weight: bold;
  }
  .dateCard{
    font-size: 12px;
  }
  .captionCard{
    margin-top: 10px;
  }
</style>
