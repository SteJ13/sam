<template>
    <div>
        <!-- Form Section -->
        <form @submit.prevent="handleSubmit">
            <label for="name">Name:</label>
            <input type="text" id="name" v-model="formData.name" required />

            <label for="email">Email:</label>
            <input type="email" id="email" v-model="formData.email" required />

            <label for="phone">Phone:</label>
            <input type="tel" id="phone" v-model="formData.phone" required />

            <label>Gender:</label>
            <label for="male">
                <input type="radio" id="male" value="male" v-model="formData.gender" />
                Male
            </label>
            <label for="female">
                <input type="radio" id="female" value="female" v-model="formData.gender" />
                Female
            </label>

            <label>Languages:</label>
            <label v-for="(language, index) in languages" :key="index">
                <input type="checkbox" :value="language" v-model="formData.languages" />
                {{ language }}
            </label>

            <label for="role">Role:</label>
            <select id="role" v-model="formData.role" required>
                <option value="" disabled>Select role</option>
                <option value="trainee">Trainee</option>
                <option value="frontend">Frontend Developer</option>
                <option value="backend">Backend Developer</option>
            </select>

            <button type="submit">Submit</button>
        </form>

        <!-- Table Section -->
        <div>
            <label for="search">Search by Name:</label>
            <input type="text" id="search" v-model="searchQuery" />

            <table>
                <thead>
                    <tr>
                        <th>Name</th>
                        <th>Email</th>
                        <th>Phone</th>
                        <th>Gender</th>
                        <th>Languages</th>
                        <th>Role</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="(entry, index) in filteredData" :key="index">
                        <td>{{ entry.name }}</td>
                        <td>{{ entry.email }}</td>
                        <td>{{ entry.phone }}</td>
                        <td>{{ entry.gender }}</td>
                        <td>{{ entry.languages.join(', ') }}</td>
                        <td>{{ entry.role }}</td>
                    </tr>
                </tbody>
            </table>
        </div>
    </div>
</template>
  
<script>
export default {
    name: "FormComponent",
    data() {
        return {
            formData: {
                name: "",
                email: "",
                phone: "",
                gender: "",
                languages: [],
                role: "",
            },
            languages: ["English", "French", "Spanish"],
            searchQuery: "",
        };
    },
    computed: {
        filteredData() {
            return this.data.filter((entry) =>
                entry.name.toLowerCase().includes(this.searchQuery.toLowerCase())
            );
        },
    },
    methods: {
        submitForm() {
            // Perform form validation
            if (!this.formData.name || !this.formData.email || !this.formData.phone || !this.formData.gender || !this.formData.role) {
                alert("Please fill in all required fields.");
                return;
            }

            // Perform additional validations as needed

            // Add the form data to the table
            this.data.push({ ...this.formData });
        },
    },
};
</script>
  