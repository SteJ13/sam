<template>
    <div>
        <button @click="toggleView">{{ showForm ? "Show Table" : "Show Form" }}</button>

        <div v-if="showForm">
            form compo
            <FormComponent />
        </div>
        <div v-else>
            <!-- <TableComponent :data="formData" :search-query="searchQuery" /> -->
            table compo
        </div>
    </div>
</template>

<script>
import FormComponent from "@/components/Employees/FormComponent.vue";


export default {
    data() {
        return {
            showForm: false,
            formData: [],
            searchQuery: ""
        }
    },
    methods: {
        toggleView() {
            this.showForm = !this.showForm
        },
        handleSubmit(formData) {
            console.log('formData: ', formData);
            // Handle form submission and add data to the table
            this.formData.push({ ...formData });
            // Optionally, you can reset the form or perform other actions after submission
            // this.showForm = false; // Uncomment this line to automatically switch to the table after submission
        },
    }
}
</script>
