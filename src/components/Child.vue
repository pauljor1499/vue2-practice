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
                    :disabled="hasData"
                >
                    Clear
                </v-btn>
                <v-btn
                    color="primary"
                    @click="addStudent()"
                    :disabled="hasData"
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
import _ from "lodash";

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

            //passing object to object
            Object.keys(this.students[index]).forEach((key) => {
                this.input_student[key] = this.students[index][key];
                this.old_student[key] = this.students[index][key];
            });
        },

        addStudent() {
            const new_student = {
                first_name: this.input_student.first_name,
                middle_name: this.input_student.middle_name,
                last_name: this.input_student.last_name,
            };

            if (
                this.input_student.first_name != "" &&
                this.input_student.middle_name != "" &&
                this.input_student.last_name != ""
            ) {
                if (!this.isExists(new_student)) {
                    this.students.push(new_student);
                    this.resetFields();
                }
            }
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

        isExists(input_obj) {
            for (const item in this.students) {
                // console.log(_.isEqual(this.students[item], input_obj));

                //do not put return false. just to target the true value
                if (
                    JSON.stringify(this.students[item]) ==
                    JSON.stringify(input_obj)
                ) {
                    console.log("true");
                    return true;
                }
            }
        },

        resetFields() {
            this.selected_index = -1;

            const reset_fields = {
                first_name: "",
                middle_name: "",
                last_name: "",
            };

            Object.keys(reset_fields).forEach((key) => {
                this.input_student[key] = reset_fields[key];
                this.old_student[key] = reset_fields[key];
            });
        },
    },

    computed: {
        hasSelected() {
            if (this.selected_index != -1) {
                return true;
            } else {
                return false;
            }
        },

        validateData() {
            if (
                JSON.stringify(this.input_student) ==
                    JSON.stringify(this.old_student) ||
                this.selected_index < 0
            ) {
                return true;
            }
            return false;
        },

        hasData() {
            if (
                this.input_student.first_name == "" &&
                this.input_student.middle_name == "" &&
                this.input_student.last_name == ""
            ) {
                return true;
            } else {
                return false;
            }
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
}

td {
    padding: 20px;
    border: 1px solid #c9c9c9;
}
</style>
