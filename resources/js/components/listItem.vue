<template>
		<section class="todo-list">
			<div class="list" id="todo-list">
				<div :class="`todo-item ${item.completed && 'done'}`">
					<label>
						<input type="checkbox" v-model="item.completed" />
						<span :class="`bubble ${
							item.completed
								? 'true' 
								: 'false'
						}`"></span>
					</label>
					<div class="todo-content">
						<input type="text" v-model="item.name" />
					</div>
					<div class="actions">
                        <button class="edit" @click="updateCheck()">Edit</button>
						<button class="delete" @click="removeItem()">Delete</button>
					</div>
				</div>

			</div>
		</section>
</template>

<script>
export default {
    props: ["item"],
    methods: {
        updateCheck() {
            const itemd = axios
                .put(`api/item/${this.item.id}`, {
                    item: this.item
                })
                .then(res => {
                    if (res.status == 200) {
                        this.$emit("itemchanged");
                    }
                })
                .catch(error => {
                    console.log("error from axios put", errors);
                });
                console.log(itemd);
        },
        removeItem() {
            axios
                .delete(`api/item/${this.item.id}`)
                .then(res => {
                    if (res.status == 200) {
                        this.$emit("itemchanged");
                    }
                })
                .catch(error => {
                    console.log("error from axios delte ", error);
                });
        }
    }
};
</script>

<style>
.completed {
    text-decoration: line-through;
    color: gray;
}
.item {
    word-break: break-all;
}
</style>