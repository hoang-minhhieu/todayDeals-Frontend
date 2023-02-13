<style scoped lang="scss">
.my-card {
  height: 200px;
  display: grid;
  grid-template-columns: 50px 1fr 3fr;
}

.q-card--bordered {
  border: 3px solid rgba(0, 0, 0, 0.12);
  border-radius: 5px;
}

.voteDeals {
  grid-column: 1;
  grid-row-start: 1;
  grid-row-end: 5;
  display: contents;
}

.voteCount {
  text-align: center;
  align-self: center;
  font-weight: bold;
}

.voteBtn {
  padding: 0;
}

.dealImg {
  grid-column: 2;
  grid-row-start: 1;
  grid-row-end: 5;
}

.cardContents {
  grid-column: 3;
  display: grid;
  grid-row-start: 1;
  grid-row-end: 5;
  padding: 10px;
  grid-template-rows: 1fr 0.5fr 1fr 0.5fr;
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

.shipmentCost {
  display: flex;
  margin-left: 10px;
}

.description {
  grid-row: 3;
  text-overflow: ellipsis;
}

.lastRowBtns {
  display: flex;
  grid-row: 4;
  .q-btn {
    margin-left: 15px;
    height: 25px;
    align-self: center;
  }
}

.expireDate {
  align-self: center;
  color: red;
  font-weight: bold;
  margin-left: auto;
}
</style>
<template>
  <q-scroll-area class="fit">
    <q-infinite-scroll @load="onLoad" :offset="250">
      <div v-for="(item, index) in items" :key="index" class="caption">
        <q-card flat bordered>
          <q-card-section class="my-card" horizontal>
            <q-card-section class="voteDeals">
              <div style="display: grid">
                <q-btn
                  class="voteBtn"
                  flat
                  color="red"
                  @click="upvote"
                  icon="add"
                  size="large"
                />
                <div
                  class="voteCount"
                  :style="{ color: voteCount > 0 ? 'red' : '#1976D2' }"
                >
                  {{ voteCount == 0 ? 'Vote' : `${voteCount}°` }}
                </div>
                <q-btn
                  class="voteBtn"
                  flat
                  color="primary"
                  @click="downvote"
                  icon="remove"
                  size="large"
                />
              </div>
            </q-card-section>
            <q-card-section class="dealImg">
              <q-img
                src="https://cdn.quasar.dev/img/parallax2.jpg"
                style="position: initial"
              />
            </q-card-section>
            <q-card-section class="cardContents">
              <div class="title ellipsis">
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
              <div class="description ellipsis">
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
                  <div class="timeDiff">{{ timeDiff }}</div>
                </div>
                <div class="expireDate">HSD: {{ expire }}</div>
                <q-btn
                  color="primary"
                  @click="downvote"
                  label="Lưu"
                  icon="bookmark"
                />
                <q-btn
                  color="primary"
                  @click="downvote"
                  label="Xem"
                  icon="open_in_new"
                />
              </div>
            </q-card-section>
          </q-card-section>
        </q-card>
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
import dayjs from 'dayjs';
import relativeTime from 'dayjs/plugin/relativeTime';
import vi from 'dayjs/locale/vi';
export default defineComponent({
  name: 'DealsCardComponent',
  components: {},

  setup() {
    const items = ref([{}, {}, {}, {}, {}, {}, {}]);
    const voteCount = ref(0);
    const expire = '05/02/2023';
    dayjs.extend(relativeTime);
    const timeDiff = dayjs(dayjs(expire).format('DD/MM/YYYY'))
      .locale(vi)
      .fromNow();
    const title = 'Sản phẩm mẫu';
    const price_with_discount = 50000;
    const price_without_discount = 100000;
    const shipment = 5000;
    const description = 'Đây là phần thông tin sản phẩm';
    const author = 'Bánh Bèo';
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
      timeDiff,
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
