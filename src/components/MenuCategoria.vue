<template>
  <div class="menu-categoria">
      <div :key="category.id" v-for="category in categories" class="menu">
            <div class="category-name" @click="selectCategory(category.id)">
              {{category.name}}
            </div>
      </div>
  </div>
</template>

<script>
import EventBus from '../eventBus.js'

    export default {
        data: () => ({
            categories: {
                id: 0,
                name: ''
            }
        }),
        methods: {
            getCategories() {
                this.$http.get(process.env.VUE_APP_API + 'categories/').then(
                    success => {
                        if (success.status === 200) {
                        this.categories = success.body
                        }
                    }, 
                    failure => {
                        console.log(failure)
                        alert("erro")
                    }
                )
            },
            selectCategory(value) {
                EventBus.$emit('selectCategory', value)
            }
        },
        mounted() {
            this.getCategories()
        }
    }

</script>

<style>

.menu-categoria {
    background-color: rgba(68, 68, 68, 0.7);
    color: whitesmoke;
    position: fixed;
    width: 12%;
    z-index: 10;
    height: 100%;
}

.category-name {
    margin-bottom: 15px;
    text-align: center;
    font-size: 20px;
    user-select: none;
    cursor: pointer;
}

</style>