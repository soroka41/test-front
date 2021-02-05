<template>
  <div class="home">
    <div class="container">
      <div class="row">
        <div class="col-12">
          <div class="form-group">
            <h5 class="card-title mb-3">Продукт A</h5>
            <input type="text" class="form-control" placeholder="Написать ваш комментарий" v-model="commitInput">
            <div class="action-blocks" v-if="commitInput !== ''">
              <button @click.prevent="addCommit"  class="btn btn-primary m-3">Сохранить</button>
              <button @click.prevent="updateCommit"  class="btn btn-light">Отмена</button>
            </div>
            <div v-if="alert" class="alert alert-primary" role="alert">
              Поле не должны быть пустым
            </div>
          </div>
          <div v-if="commit.length">
            <card
              v-for="(card, idx) in commit"
              :key="idx"
              :cardIdx="idx"
              :card="card"
              @deleteCommit="deleteCommit"
              @updateCommit="updateCommit"
            ></card>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import card from '@/components/card.vue'
export default {
  data: () =>({
    alert: false,
    commit: [],
    commitInput: ''
  }),
  components: {
    card
  },
  methods: {
    deleteCommit(data) {
      let success = confirm("Удалить")
      if(success)
        this.commit = this.commit.filter((i, idx) => idx !== data)
    },
    updateCommit() {
    },
    addCommit() {
      this.alert = false
      if(this.commitInput !== '') {
        let commitItem = {}
        commitItem.date_commit = new Date().toLocaleString()
        commitItem.text_commit = this.commitInput
        commitItem.user_commit = 'Петя'
        this.commit.unshift(commitItem)
        this.commitInput = ''
        console.log(this.commit)
      } else {
        this.alert = true
      }
    }
  }
}
</script>
<style lang="scss">
  .home {
    margin: 0 auto;
    width: 700px;
    padding: 40px;
  }
</style>
