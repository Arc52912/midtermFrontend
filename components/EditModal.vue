<template>
    <div>

        <b-modal id="editModal" title="Movie Entry" ok-title="Save" @ok="onSubmit">
            <form action="#">
                <b-form-group
                    label="Laptop Name"
                    label-for="laptop_name"
                    >
                    <b-form-input id="laptop_name" v-model="asset.laptop_name" trim></b-form-input>
                </b-form-group>

                <b-form-group
                    label="Description"
                    label-for="description"
                    >
                    <b-form-input id="description" v-model="asset.description" trim></b-form-input>
                </b-form-group>

                <b-form-group
                    label="OS"
                    label-for="os"
                    >
                    <b-form-input id="os" v-model="asset.os" trim></b-form-input>
                </b-form-group>

                <b-form-group
                    label="Price"
                    label-for="price"
                    >
                    <b-form-input id="price" v-model="asset.price" trim></b-form-input>
                </b-form-group>

                <b-form-group
                    label="Date"
                    label-for="acquired_on"
                    >
                    <b-form-input id="acquired_on" type="date" v-model="asset.acquired_on" trim></b-form-input>
                </b-form-group>

                <b-form-group
                    label="Status"
                    label-for="status"
                    >
                    <b-form-select id="status" v-model="asset.status" :options="statuses"></b-form-select>
                </b-form-group>

            </form>
        </b-modal>
    </div>
</template>

<script>
export default {
    props: {
        asset: {}

    },
    
    data() {
        return {
            asset: {},
            statuses: [
                { value: 'good', text: 'Good' },
                { value: 'very good', text: 'Very Good' },
                { value: 'excellent', text: 'Excellent' },
                
            ]
        }
    },
    methods: {
        async onSubmit() {
            this.$axios.put('http://localhost:8000/api/assets/' + this.asset.id, this.asset)
            .then((res)=>{
                if(res.status==202) {
                    alert('Update Successfully')
                }
            })
            .catch((err)=>{
                alert(err.message)
            })
        }
    }
    
}
</script>