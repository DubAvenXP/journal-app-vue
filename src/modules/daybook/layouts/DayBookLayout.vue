<template>
    <Navbar />
    <div v-if="isLoading" class="row justify-content-center">
        <div class="col-3 alert-info text-center mt-5">
            Espere por favor...
            <h3 class="mt-2">
                <i class="fa fa-spin fa-sync"></i>
            </h3>
        </div>
    </div>
    <div class="d-flex" v-else  >
        <EntryList />
        <div class="col">
            <router-view></router-view>
        </div>
    </div>
</template>

<script>
import { defineAsyncComponent } from "vue";
import { mapActions, mapState } from "vuex";
export default {
    components: {
        Navbar: defineAsyncComponent(() => import("../components/Navbar.vue")),
        EntryList: defineAsyncComponent(() =>
            import("../components/EntryList.vue")
        ),
    },
    created() {
        this.loadEntries();
    },
    methods: {
        ...mapActions("journal", ["loadEntries"]),
    },
    computed: {
        ...mapState("journal", ["isLoading"]),
    },
};
</script>

<style></style>
