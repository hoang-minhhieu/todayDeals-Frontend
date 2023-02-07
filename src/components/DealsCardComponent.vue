<style scoped lang="scss">
.cardContents {
  display: grid;
  grid-template-rows: 1fr 1fr 1.5fr 1fr;
}

.voteDeals {
  border: 2px solid black;
  width: fit-content;
  border-radius: 5px;
  margin: 15px 20px 15px 0px;
  right: 0;
  position: absolute;
  display: flex;
  width: 130px;
}

.voteCount {
  text-align: center;
  align-self: center;
  font-weight: bold;
}

.voteBtn {
  padding: 0;
}

.author {
  align-self: center;
  display: flex;
}

.timeDiff {
  align-self: center;
}

.title {
  font-size: 1.5rem;
  font-weight: bold;
  grid-row: 1;
}

.prices {
  display: flex;
  font-size: 1.3rem;
  align-items: center;
  align-self: center;
  margin-bottom: 10px;
  grid-row: 2;
}

.discountPrice {
  font-weight: 500;
  background: #f7941d;
  display: inline-block;
  color: #fff;
  padding: 2px 18px;
  border-radius: 30px;
}

.fullPrice {
  text-decoration: line-through;
  color: grey;
  margin: 0 10px;
}

.discountPercentage {
}

.shipmentCost {
  display: flex;
  margin-left: 10px;
}

.description {
  grid-row: 3;
}

.lastRowBtns {
  display: flex;
  grid-row: 4;
}

.expireDate {
  align-self: center;
  color: red;
  font-weight: bold;
  margin-left: auto;
}

.my-card {
  height: 220px;
}

.q-card--bordered {
  border: 3px solid rgba(0, 0, 0, 0.12);
  border-radius: 5px;
}
</style>
<template>
  <q-scroll-area class="fit">
    <q-infinite-scroll @load="onLoad" :offset="250">
      <div v-for="(item, index) in items" :key="index" class="caption">
        <div class="cards-area">
          <q-card flat bordered>
            <q-card-section class="my-card" horizontal>
              <q-card-section class="col-3">
                <q-img
                  src="https://cdn.quasar.dev/img/parallax2.jpg"
                  style="position: initial"
                />
              </q-card-section>
              <q-card-section class="col-9 cardContents">
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
                <div class="title">
                  {{ title }}
                </div>
                <div class="prices">
                  <div class="discountPrice">{{ price_with_discount }}</div>
                  <div class="fullPrice">{{ price_without_discount }}</div>
                  <div class="discountPercentage">
                    (Giảm {{ discount_percentage }}%)
                  </div>
                  <div class="shipmentCost">
                    <q-icon
                      name="local_shipping"
                      style="font-size: xx-large"
                    ></q-icon
                    >{{ shipment }}
                  </div>
                </div>
                <div class="description">
                  {{ description }}
                </div>
                <div class="lastRowBtns">
                  <div class="author">
                    <q-chip>
                      <q-avatar>
                        <img :src="avatar" />
                      </q-avatar>
                      {{ author }}
                    </q-chip>
                    <div class="timeDiff">{{ today }}</div>
                  </div>
                  <div class="expireDate">HSD: {{ expire }}</div>
                  <q-btn
                    color="primary"
                    @click="downvote"
                    label="Chia sẻ"
                    icon="share"
                    style="margin-left: 15px"
                  />
                  <q-btn
                    color="primary"
                    @click="downvote"
                    label="Xem thêm"
                    icon="open_in_new"
                    style="margin-left: 15px"
                  />
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
    const expire = '05/02/2023';
    const title = 'Tên sản phẩm';
    const price_with_discount = 50000;
    const price_without_discount = 100000;
    const shipment = 5000;
    const description = 'This is a description';
    const author = 'James';
    const discount_percentage = Math.round(
      (price_with_discount / price_without_discount) * 100,
    );
    const avatar = ref('https://cdn.quasar.dev/img/avatar.png');

    function upvote() {
      voteCount.value++;
    }

    function downvote() {
      voteCount.value--;
    }

    function toCurrency(value: number) {
      var formatter = new Intl.NumberFormat('de-DE', {
        style: 'currency',
        currency: 'VND',
      });
      return formatter.format(value);
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
      avatar,
      expire,
      today: today.replace(/(\d+)\/(\d+)\/(\d+)/, '$2/$1/$3'),
      title,
      price_with_discount: toCurrency(price_with_discount),
      price_without_discount: toCurrency(price_without_discount),
      discount_percentage,
      shipment: toCurrency(shipment),
      description,
      author,
    };
  },
});
</script>
