<template>
    <div class="container">
        <h2 class="text-center">Editando produto</h2>
        <div class="row">
            <div class="col-md-12">
                <router-link :to="{ name: 'ProductIndex' }" class="btn btn-primary btn-sm float-right mb-2">Voltar</router-link>
            </div>
        </div>
        <div class="row">
            <div class="col-md-12">
                <form>
                    <div class="form-group">
                        <label>Nome</label>
                        <input type="text" class="form-control" v-model="product.name">
                    </div>
                    <div class="form-group">
                        <label>Descrição</label>
                        <textarea type="text" rows="5" class="form-control" v-model="product.description"></textarea>
                    </div>
                    <div class="form-group">
                        <label>Preço</label>
                        <input type="text" class="form-control" v-model="product.price">
                    </div>
                    <button type="button" class="btn btn-primary" @click="updateProduct()"> Update </button>
                </form>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                product: {}
            }
        },
        mounted() {
            this.editProduct(this.$route.params.productId);
        },
        methods: {
            editProduct(productId) {
                this.axios.get(`http://127.0.0.1:8000/api/products/${productId}`)
                   .then((res) => {
                       this.product = res.data;
                   });
            },
            updateProduct() {
                this.axios
                    .patch(`http://127.0.0.1:8000/api/products/${this.$route.params.productId}`, this.product)
                    .then((res) => {
                        this.$router.push({ name: 'ProductIndex' });
                    });
            }
        }
    }
</script>