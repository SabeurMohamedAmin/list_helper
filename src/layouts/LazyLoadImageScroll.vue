<script>
export default {
  name: "LazyLoadImageScroll",
  data: () => ({
    inView: Array.apply(null, Array(50)).map(_ => false),
  }),
  methods: {
    onIntersection(entry) {
      const index = parseInt(entry.target.dataset.id, 10)
      setTimeout(() => {
        this.inView.splice(index, 1, entry.isIntersecting)
      }, 50)
    }
  }
}
</script>


<template>
  <div class="q-pa-md">
    <div class="row justify-center q-gutter-sm">
      <div
        v-for="index in inView.length"
        :key="index"
        :data-id="index - 1"
        class="example-item q-pa-sm flex flex-center relative-position"
        v-intersection="onIntersection"
      >
        <transition name="q-transition--scale">
          <q-card v-if="inView[index - 1]">
            <img src="https://cdn.quasar.dev/img/mountains.jpg">

            <q-card-section>
              <div class="text-h6">Card #{{ index }}</div>
              <div class="text-subtitle2">by John Doe</div>
            </q-card-section>
          </q-card>
        </transition>
      </div>
    </div>
  </div>
</template>


<style scoped>

</style>


<style scoped>
.example-item{
  height: 290px;
  width: 290px;
}

</style>

