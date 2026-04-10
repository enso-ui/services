<template>
    <div class="wrapper">
        <div class="columns is-centered is-multiline">
            <div class="column is-narrow">
                <boolean-filter class="box"
                    :name="i18n('Active')"
                    v-model="filters.services.is_active"/>
            </div>
            <div class="column is-narrow">
                <boolean-filter class="box"
                    :name="i18n('Additional')"
                    v-model="filters.services.is_additional"/>
            </div>
            <div class="column is-narrow">
                <boolean-filter class="box"
                    :name="i18n('Contractor Exclusive')"
                    v-model="filters.services.is_contractor_exclusive"/>
            </div>
        </div>
        <enso-table class="box p-0"
            v-model:filters="filters"
            :filter-version="1.1"
            id="services"/>
    </div>
</template>

<script setup>
import { ref, inject } from 'vue';
import { BooleanFilter } from '@enso-ui/filters/bulma';
import { EnsoTable } from '@enso-ui/tables/bulma';

const i18n = inject('i18n');
const filters = ref({
    services: {
        is_active: null,
        is_additional: null,
        is_contractor_exclusive: null,
    },
});
</script>
