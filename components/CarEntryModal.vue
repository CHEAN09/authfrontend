<template>
    <div>
        <b-button v-b-modal.carsEntryModal variant="primary">Add Car</b-button>

        <b-modal id="carsEntryModal" title="Car Entry" ok-title="Save Car" @ok="onSubmit">
            <form action="#">
                <b-form-group label="Name" label-for="name">
                <b-form-input id="name" v-model="cars.name" trim></b-form-input>
                </b-form-group>

                <b-form-group label="Description" label-for="description">
                <b-form-input id="description" v-model="cars.description" trim></b-form-input>
                </b-form-group>

                <b-form-group label="Brand" label-for="brand">
                <b-form-input id="brand" v-model="cars.brand" trim></b-form-input>
                </b-form-group>

                <b-form-group label="Date Acquired" label-for="acquired_on">
                <b-form-input id="acquired_on" type="date" v-model="cars.acquired_on" trim></b-form-input>
                </b-form-group>

                <b-form-group label="Status" label-for="status">
                <b-form-select v-model="cars.status" :options="options"></b-form-select>
                </b-form-group>
            </form>
        </b-modal>
    </div>
</template>

<script>
export default {
    data() {
        return {
            cars: {},
            options: [
                {value: 'good', text: 'In good condition'},
                {value: 'damaged', text: 'Damaged'},
                {value: 'lost', text: 'Lost'},
            ]
        }
    },
    methods: {
        async onSubmit() {
            this.$axios.post('/api/cars', this.cars)
            .then((res)=>{
                if(res.status==202) {
                    alert('Successfully added a car')
                    this.$emit('onAdd')
                }
            })
        }
    }
}
</script>