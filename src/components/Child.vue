<template>
    <div class="main-content">
        <div class="actions">
            <v-text-field outlined dense label="First name"> </v-text-field>
            <v-text-field outlined dense label="Middle name"> </v-text-field>
            <v-text-field outlined dense label="Last name"> </v-text-field>

            <div class="action-buttons">
                <v-btn color="primary"> Clear </v-btn>
                <v-btn color="primary">
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
                    <tr>
                        <td>Jose</td>
                        <td>Sample</td>
                        <td>Rizal</td>
                        <td>
                            <v-btn color="red"> view </v-btn>
                        </td>
                    </tr>
                    <tr>
                        <td>Jose</td>
                        <td>Sample</td>
                        <td>Rizal</td>
                        <td>
                            <v-btn color="red"> view </v-btn>
                        </td>
                    </tr>
                    <tr>
                        <td>Jose</td>
                        <td>Sample</td>
                        <td>Rizal</td>
                        <td>
                            <v-btn color="red"> view </v-btn>
                        </td>
                    </tr>
                </tbody>
            </table>
        </div>
    </div>
</template>

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
