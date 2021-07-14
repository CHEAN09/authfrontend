<template>
    <div>
        <b-modal id="editCarModal" title="Edit Car" ok-title="Save car" @ok="onSubmit">
            <form action="#">
                <b-form-group label="Name" label-for="name">
                <b-form-input id="name" v-model="cars.name" trim></b-form-input>
                </b-form-group>

                <b-form-group label="Description" label-for="description">
                <b-form-input id="description" v-model="cars.description" trim></b-form-input>
                </b-form-group>

                <b-form-group label="Brand" label-for="brand">
                <b-form-input id="brand" v-model="cars.location" trim></b-form-input>
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
    props: {
        cars: {}
    },
    data() {
        return {
            options: [
                {value: 'good', text: 'In good condition'},
                {value: 'damaged', text: 'Damaged'},
                {value: 'lost', text: 'Lost'},
            ]
        }
    },
    methods: {
        async onSubmit() {
            this.$axios.put('https://lentrix.tk/verano/api/cars/' + this.cars.id, this.cars)
            .then((res)=>{
                if(res.status==202) {
                    alert('Edit successful!')
                }
            })
            .catch((err)=>{
                alert(err.message)
            })
        }
    }
}
</script>