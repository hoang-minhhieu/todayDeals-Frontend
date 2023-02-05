<style scoped>
.voteDeals {
  border: 2px solid black;
  width: fit-content;
  border-radius: 5px;
  margin: 15px 30px 15px 0px;
  right: 0;
  top: 0;
  position: absolute;
  display: flex;
  width: 110px;
}

.voteCount {
  text-align: center;
  align-self: center;
  font-weight: bold;
}

.voteBtn {
  padding: 0;
}

.my-card {
  height: 230px;
}
</style>
<template>
  <q-scroll-area class="fit">
    <q-infinite-scroll @load="onLoad" :offset="250">
      <div v-for="(item, index) in items" :key="index" class="caption">
        <div class="cards-area">
          <q-card class="my-card" flat bordered>
            <q-card-section horizontal>
              <q-card-section class="col-3">
                <q-img src="https://cdn.quasar.dev/img/parallax2.jpg" />
                <div>Đăng bởi {{ author }} {{ today }}</div>
              </q-card-section>
              <q-card-section class="col-9">
                <div>
                  <p>Hết hạn: {{ expire }}</p>
                  <div class="voteDeals row">
                    <q-btn
                      class="voteBtn col-4"
                      flat
                      color="primary"
                      @click="downvote"
                      icon="ac_unit"
                    />
                    <div
                      class="voteCount col-4"
                      :style="{ color: voteCount > 0 ? 'red' : '#1976D2' }"
                    >
                      {{ voteCount == 0 ? 'Vote' : `${voteCount}°` }}
                    </div>
                    <q-btn
                      class="voteBtn col-4"
                      flat
                      color="red"
                      @click="upvote"
                      icon="local_fire_department"
                    />
                  </div>
                  <div>
                    {{ title }}
                  </div>
                  <div>
                    {{ price_with_discount }} {{ price_without_discount }}
                  </div>
                  <div>
                    {{ shipment }}
                  </div>
                  <div>
                    {{ description }}
                  </div>
                </div>
              </q-card-section>
            </q-card-section>
          </q-card>
        </div>
      </div>
      <template v-slot:loading>
        <div class="row justify-center q-my-md">
          <q-spinner-dots color="primary" size="40px" />
        </div>
      </template>
    </q-infinite-scroll>
  </q-scroll-area>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import { ref } from 'vue';
export default defineComponent({
  name: 'DealsCardComponent',
  components: {},

  setup() {
    const items = ref([{}, {}, {}, {}, {}, {}, {}]);
    const voteCount = ref(0);
    const today = new Date().toLocaleDateString('vn-VN', {
      day: '2-digit',
      month: '2-digit',
      year: 'numeric',
    });

    function upvote() {
      voteCount.value++;
    }

    function downvote() {
      voteCount.value--;
    }

    return {
      items,
      voteCount,
      upvote,
      downvote,
      onLoad(index: number, done: () => void) {
        setTimeout(() => {
          items.value.push({}, {}, {}, {}, {}, {}, {});
          done();
        }, 2000);
      },
      expire: '05/02/2023',
      today: today.replace(/(\d+)\/(\d+)\/(\d+)/, '$2/$1/$3'),
      title: 'Tên sản phẩm',
      price_with_discount: '5€',
      price_without_discount: '10€',
      shipment: '5€',
      description: 'This is a description',
      author: 'James',
    };
  },
});
</script>
