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
                <v-btn
                    color="primary"
                    @click="resetFields()"
                    :disabled="!hasSelected"
                >
                    Clear
                </v-btn>
                <v-btn
                    color="primary"
                    @click="addStudent()"
                    :disabled="hasSelected"
                >
                    <v-icon dark> mdi-plus </v-icon>Add
                </v-btn>
                <v-btn
                    color="green"
                    @click="updateStudent()"
                    :disabled="validateData"
                >
                    <v-icon dark color="white"> mdi-update </v-icon>
                    Update
                </v-btn>
                <v-btn
                    color="red"
                    @click="removeStudent()"
                    :disabled="!hasSelected"
                >
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

                <tbody v-if="this.students != ''">
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

                <tbody v-else>
                    <h1>No Array Data</h1>
                </tbody>
            </table>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            selected_index: -1,

            input_student: {
                first_name: "",
                middle_name: "",
                last_name: "",
            },

            old_student: {
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

            this.old_student.first_name = this.students[index].first_name;
            this.old_student.middle_name = this.students[index].middle_name;
            this.old_student.last_name = this.students[index].last_name;
        },

        addStudent() {
            const new_student = {
                first_name: this.input_student.first_name,
                middle_name: this.input_student.middle_name,
                last_name: this.input_student.last_name,
            };

            this.students.push(new_student);
            this.resetFields();
        },

        updateStudent() {
            const update_student = {
                first_name: this.input_student.first_name,
                middle_name: this.input_student.middle_name,
                last_name: this.input_student.last_name,
            };

            this.students.splice(this.selected_index, 1, update_student);
            this.resetFields();
        },

        removeStudent() {
            this.students.splice(this.selected_index, 1);
            this.resetFields();
        },

        resetFields() {
            this.selected_index = -1;
            this.input_student.first_name = "";
            this.input_student.middle_name = "";
            this.input_student.last_name = "";

            JSON.stringify((this.input_student = ""));
            JSON.stringify((this.old_student = ""));
        },
    },

    computed: {
        hasSelected() {
            if (this.selected_index != -1) {
                return true;
            }
        },

        validateData() {
            if (
                JSON.stringify(this.input_student) ===
                JSON.stringify(this.old_student)

                // this.input_student.first_name === this.old_student.first_name &&
                // this.input_student.middle_name ===
                //     this.old_student.middle_name &&
                // this.input_student.last_name === this.old_student.last_name
            )
                return true;
        },
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
