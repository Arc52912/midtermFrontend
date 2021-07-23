<template>
    <div>
        <NavBar />

        <div class="container">
            <EditModal :asset="selectedAsset" />
            <DeleteModal :asset="selectedAsset" @onDeleted="getAll" />
            
            <h1>
                <LaptopEntryModal class="float-right" @onAdd="getAll" />
                Laptop
            </h1>

            <table class="table table-boredered">
                <thead>
                    <tr class="bg-info text-white">
                        <th>Laptop Name</th>
                        <th>Description</th>
                        <th>OS</th>
                        <th>Price</th>
                        <th>Status</th>
                        <th>&nbsp;</th>
                        <th>&nbsp;</th>
                    </tr>
                </thead>

                <tbody>
                    <tr v-for="asset in assets" :key="asset.id">
                        <td>{{asset.laptop_name}}</td>
                        <td>{{asset.description}}</td>
                        <td>{{asset.director}}</td>
                        <td>{{asset.counrty}}</td>
                        <td>{{asset.status}}</td>
                        <td>
                            <b-button @click="onEdit(asset)" variant="info" size="sm">Edit</b-button>
                        </td>
                        <td>
                            <b-button @click="onDelete(asset)" variant="danger" size="sm">Delete</b-button>
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
            assets: [],
            selectedAsset: {}
        }
    },
    methods: {
        async getAll() {
            await this.$axios.get('http://localhost:8000/api/assets')
            .then((res)=>{
                if(res.status==200) {
                    this.assets = res.data
                    console.log(this.assets)
                }
            })
        },
        onEdit(selectedAsset) {
            this.selectedAsset = selectedAsset;
            this.$bvModal.show('editModal')
        },
        onDelete(selectedAsset) {
            this.selectedAsset = selectedAsset;
            this.$bvModal.show('deleteModal')
        }
    },
    created() {
        this.getAll()
    }
}
</script>