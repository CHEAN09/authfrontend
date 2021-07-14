<template>
    <div>
        <NavBar />
        <EditCarModal :cars="selectedCars" />
        <DeleteCarModal :cars="selectedCars" @onDeleted="getAll" />

        <div class="container">
            <h1>
               Cars
            </h1>
            
            <CarEntryModal class="float-right mb-1" @onAdd="getAll" />

            <table class="table table-bordered table-striped table-primary">
                <thead>
                    <tr class="bg-info text-white">
                        <th>Name</th>
                        <th>Description</th>
                        <th>Brand</th>
                        <th>Status</th>
                        <th>&nbsp;</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="cars in cars" :key="cars.id">
                        <td>{{cars.name}}</td>
                        <td>{{cars.description}}</td>
                        <td>{{cars.brand}}</td>
                        <td>{{cars.status}}</td>
                        <td class="buttons">
                            <b-button @click="onEdit(cars)" variant="primary" size="sm">
                                Edit
                            </b-button>
                            <b-button @click="onDelete(cars)" variant="danger" size="sm">
                                Delete
                            </b-button>
                        </td>
                    </tr>
                </tbody>
            </table>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            cars: [],
            selectedCars: {}
        }
    },
    methods: {
        async getAll() {
            await this.$axios.get('/api/cars')
            .then((res)=>{
                if (res.status==200) {
                    this.cars = res.data
                }
            })
        },
        onEdit(selectedCars) {
            this.selectedCars = selectedCars
            this.$bvModal.show('editCarModal')
        },
        onDelete(selectedCars) {
            this.selectedCars = selectedCars
            this.$bvModal.show('deleteCarModal')
        }
    },
    created() {
        this.getAll()
    }
}
</script>

<style>
h1 {
    text-align: center;
    margin-top: 50px;
}
.buttons {
    text-align: center;
}
</style>