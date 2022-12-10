<template>
    <div class="container">
        <h2 class="text-center">Lista de produtos</h2>
        <div class="row">
            <div class="col-md-12">
                <router-link :to="{ name: 'ProductCreate' }" class="btn btn-primary btn-sm float-right mb-2">Adicionar Produto</router-link>
            </div>
        </div>
        <div class="row">
            <div class="col-md-12">
                <table class="table">
                    <thead>
                    <tr>
                        <th>#</th>
                        <th>Nome</th>
                        <th>Descrição</th>
                        <th>Preço</th>
                        <th>Ações</th>
                    </tr>
                    </thead>
                    <tbody>
                        <tr v-for="(product, key) of products" v-bind:key="key">
                            <td>{{ key+1 }}</td>
                            <td>{{ product.name }}</td>
                            <td>{{ product.description }}</td>
                            <td>{{ product.price }}</td>
                            <td>
                                <router-link class="btn btn-success btn-sm" :to="{ name: 'ProductEdit', params: { productId: product.id }}">Editar</router-link>
                                <button class="btn btn-danger btn-sm" @click="deleteProduct(product.id)">Deletar</button>
                            </td>
                            <td>
                            </td>
                        </tr>
                    </tbody>
                </table>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                products: {}
            }
        },
        created() {
            this.getProducts();
        },
        methods: {
            getProducts() {
              this.axios.get('http://127.0.0.1:8000/api/products')
                  .then(response => {
                      this.products = response.data;
                  });
            },
            deleteProduct(productId) {
                this.axios
                    .delete(`http://127.0.0.1:8000/api/products/${productId}`)
                    .then(response => {
                        let i = this.products.map(data => data.id).indexOf(productId);
                        this.products.splice(i, 1)
                    });
            }
        }
    }
</script>