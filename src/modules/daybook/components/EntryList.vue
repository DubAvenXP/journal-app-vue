<template>
    <div class="entry-list-container">
        <div class="px-2 pt-2">
            <input
                type="text"
                class="form-control"
                placeholder="Buscar entrada"
                v-model="term"
            />
        </div>

        <div class="mt-2 d-flex flex-column">
            <button
                @click="$router.push({ name: 'entry', params: { id: 'new' } })"
                class="btn btn-primary mx-3"
            >
                <i class="fa fa-plus-circle"></i>
                Nueva entrada
            </button>
        </div>

        <div class="entry-scrollarea">
            <Entry
                v-for="entry in entriesByTerm"
                :key="entry.id"
                :entry="entry"
            />
        </div>
    </div>
</template>

<script>
import { mapGetters } from "vuex";
import { defineAsyncComponent } from "@vue/runtime-core";
export default {
    components: {
        Entry: defineAsyncComponent(() => import("./Entry.vue")),
    },
    computed: {
        ...mapGetters("journal", ["getEntriesByTerm"]),
        entriesByTerm() {
            return this.getEntriesByTerm(this.term);
        },
    },
    data() {
        return {
            term: "",
        };
    },
};
</script>

<style lang="scss" scoped>
input {
    height: 55px;
}
.entry-list-container {
    border-right: 1px solid #2c3e50;
    height: calc(100vh - 56px);
    width: 300px;
}
.entry-scrollarea {
    height: calc(100vh - 110px);
    overflow: scroll;
}
</style>
