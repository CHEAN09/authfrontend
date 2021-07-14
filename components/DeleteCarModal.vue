<template>
    <div>
        <b-modal id="deleteCarModal" title="Delete Car" ok-title="Delete Car" @ok="onDelete" ok-variant="danger">
            Are you sure in deleting this car? <br><br>
            Name: {{cars.name}} <br>
            Description: {{cars.description}}
        </b-modal>
    </div>
</template>

<script>
export default {
    props: {
        cars: {}
    },
    methods: {
        async onDelete() {
            this.$axios.delete('/api/cars/' + this.cars.id)
            .then((res)=>{
                if(res.status==202) {
                    alert('Deleted successfully!')
                    this.$emit('onDeleted')
                }
            })
        }
    }
}
</script>