<template>
    <div class="mt-3">
        <h2>Todo List</h2>
        <div class="container m-2 w-100">
            <input
                type="test"
                placeholder="Add todo"
                class="border"
                v-model="item.name"
            />
            <div class="invalid-feedback">
                Please provide a valid zip.
            </div>
            <button
                :class="[item.name ? 'btn btn-success' : 'btn btn-secondary']"
                @click="addItem()"
            >
                Add
            </button>
        </div>
    </div>
</template>
<script>
import listItem from "./listItem.vue";

export default {
    data: function() {
        return {
            item: {
                name: ""
            }
        };
    },
    methods: {
        addItem() {
            if (this.item.name == "") {
                return;
            }
            axios
                .post("api/item/store", {
                    item: this.item
                })
                .then(res => {
                    if (res.status == 201) {
                        this.item.name = "";
                        this.$emit("reloadlist");
                    }
                })
                .catch(error => {
                    console.log(error);
                });
        }
    }
};

// Example starter JavaScript for disabling form submissions if there are invalid fields
(() => {
  'use strict'

  // Fetch all the forms we want to apply custom Bootstrap validation styles to
  const forms = document.querySelectorAll('.needs-validation')

  // Loop over them and prevent submission
  Array.from(forms).forEach(form => {
    form.addEventListener('submit', event => {
      if (!form.checkValidity()) {
        event.preventDefault()
        event.stopPropagation()
      }

      form.classList.add('was-validated')
    }, false)
  })
})()

</script>

<style scoped>
.active {
    color: white;
    background-color: blue;
}
.inactive {
    color: gray;
}
</style>