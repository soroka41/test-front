<template>
  <div class="card mt-3 mb-3">
    <div class="card-body"   v-if="card">
      <p class="card-text" v-if="!showRedact">{{oldCommit !==''? oldCommit: card.text_commit}}</p>
      <div class="form-group" v-if="showRedact">
        <label for="">Отредактировать коммит</label>
        <input type="text" class="form-control" placeholder="Написать ваш комментарий" v-model="card.text_commit">
      </div>
      <div class="wrap-block-comment">
        <p>{{card.user_commit}}</p>
        <p>{{card.date_commit}}</p>
        <div class="block-card-action">
          <a @click.prevent="resetCommit" href="" class="w-100 btn btn-primary btn-sm" v-if="showRedact">Отмена</a>
          <a @click.prevent="updateCommit(card.text_commit)" href="" class="w-100 btn btn-sm" :class="[!showRedact? 'btn-primary': 'btn-warning']">{{!showRedact?'Редактировать': 'Сохранить'}}</a>
          <a @click.prevent="deleteCommit(cardIdx)" href="" class="w-100 btn btn-danger btn-sm" v-if="!showRedact">Удалить</a>
        </div>

      </div>
    </div>
  </div>
</template>

<script>
  export default {
    props: ['card', 'cardIdx'],
    name: 'card.vue',
    data: () => ({
      showRedact: false,
      commitInput: '',
      oldCommit: ''
    }),
    computed: {
      valueInput() {
        if(this.card.text_commit) {
          return this.commitInput = this.card.text_commit
        } else {
          return this.commitInput = ''
        }
      }
    },
    methods: {
      resetCommit() {
        this.showRedact =! this.showRedact

      },
      deleteCommit(cardIdx) {
        this.$emit('deleteCommit', cardIdx)

      },
      updateCommit(data) {
        console.log('update', data)
        this.oldCommit = data
        this.showRedact =! this.showRedact
        // this.$emit('updateCommit', data)
        console.log('2', this.showRedact )
      },
    }
  }
</script>
<style lang="scss">
  .block-card-action {
    display: flex;
    flex-direction: column;
    width: 150px;
    * {
      margin: 2px;
    }
  }
  .wrap-block-comment {
    margin-top: 20px;
    display: flex;
    align-items: center;
    justify-content: space-between;
  }
</style>