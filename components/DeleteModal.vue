<template>
    <div>

        <b-modal id="deleteModal" title="Delete Laptop" ok-title="Save" @ok="onDelete" ok-variant="danger">
            Are You Sure Want to delete this?
            <br>
            <br>
            <h1>{{asset.laptop_name}}</h1>
        </b-modal>

    </div>
</template>

<script>
export default {
    props: {
        asset: {}
    },
    methods: {
        async onDelete() {
            this.$axios.delete('http://localhost:8000/api/assets/' + this.asset.id)
            .then((res)=>{
                if(res.status==202) {
                    alert('Laptop is deleted Successfully')
                    this.$emit('onDeleted')
                }
            })
        }
    }
    
}
</script>