<template>
    <div class="main-content">
        <div class="actions">
            <v-text-field
                outlined
                dense
                label="First name"
                v-model="input_student.first_name"
            >
            </v-text-field>
            <v-text-field
                outlined
                dense
                label="Middle name"
                v-model="input_student.middle_name"
            >
            </v-text-field>
            <v-text-field
                outlined
                dense
                label="Last name"
                v-model="input_student.last_name"
            >
            </v-text-field>

            <div class="action-buttons">
                <v-btn color="primary"> Clear </v-btn>
                <v-btn color="primary" @click="addStudent()">
                    <v-icon dark> mdi-plus </v-icon>Add
                </v-btn>
                <v-btn color="green">
                    <v-icon dark color="white"> mdi-update </v-icon> Update
                </v-btn>
                <v-btn color="red">
                    <v-icon dark color="white"> mdi-delete </v-icon>Remove
                </v-btn>
            </div>
        </div>

        <div class="data-table">
            <div class="table-title">
                <span>Students</span>
            </div>
            <table>
                <thead>
                    <tr>
                        <td>First name</td>
                        <td>Middle name</td>
                        <td>Last name</td>
                        <td>Action</td>
                    </tr>
                </thead>

                <tbody>
                    <tr v-for="(student, index) in students" :key="index">
                        <td>{{ student.first_name }}</td>
                        <td>{{ student.middle_name }}</td>
                        <td>{{ student.last_name }}</td>
                        <td>
                            <v-btn color="red" @click="selectStudent(index)">
                                view
                            </v-btn>
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
            selected_index: "",

            input_student: {
                first_name: "",
                middle_name: "",
                last_name: "",
            },

            student: {
                first_name: "",
                middle_name: "",
                last_name: "",
            },

            students: [
                {
                    first_name: "Student 1",
                    middle_name: "",
                    last_name: "Student 1",
                },

                {
                    first_name: "Student 2",
                    middle_name: "",
                    last_name: "Student 2",
                },

                {
                    first_name: "Student 3",
                    middle_name: "",
                    last_name: "Student 3",
                },
            ],
        };
    },

    methods: {
        selectStudent(index) {
            this.selected_index = index;
            this.input_student.first_name = this.students[index].first_name;
            this.input_student.middle_name = this.students[index].middle_name;
            this.input_student.last_name = this.students[index].last_name;
        },

        addStudent() {
            const new_student = {
                first_name: this.input_student.first_name,
                middle_name: this.input_student.middle_name,
                last_name: this.input_student.last_name,
            };

            this.students.push(new_student);
        },

        // updateStudent() {
        //     const update_student = {
        //         first_name: this.input_student.first_name,
        //         middle_name: this.input_student.middle_name,
        //         last_name: this.input_student.last_name,
        //     };
        // },
    },
};
</script>

<style scoped>
.main-content {
    padding: 10%;
    display: flex;
    justify-content: space-between;
    gap: 50px;
}

.v-btn {
    color: #ffff;
}

.action-buttons {
    display: flex;
    gap: 10px;
}

.data-table {
    width: 100%;
}

table {
    width: 100%;
    border-collapse: collapse;
    border-bottom: 1px solid black;
}

td {
    padding: 20px;
}

thead tr {
    border-bottom: 1px solid black;
}

tbody tr {
    border-bottom: 1px solid black;
}
</style>
