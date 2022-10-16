<template>
    <div>
        <HeaderComponent />
        <ChildComponent />
    </div>
</template>

<script>
import ChildComponent from "../components/Child.vue";
import HeaderComponent from "../components/header.vue";

export default {
    components: {
        ChildComponent,
        HeaderComponent,
    },
};
</script>
