<template>
    <div class="container w-50 m-auto text-center mt-5 app">
        <h1 class="text-danger">Examination</h1>
        <add-item-form v-on:reloadlist="getItems()" />
        <list-view
            :items="items"
            v-on:reloadlist="getItems()"
            class="text-center"
        />
    </div>
</template>

<script>
import addItemForm from "./components/addItemForm.vue";
import listView from "./components/listView.vue";

export default {
    components: {
        addItemForm,
        listView
    },

    data: function() {
        return {
            items: []
        };
    },
    methods: {
        getItems() {
            axios
                .get("api/items")
                .then(res => {
                    this.items = res.data;
                })
                .catch(error => {
                    console.log(error);
                });
        }
    },
    created() {
        this.getItems();
    }
};
</script>

<style scoped></style>