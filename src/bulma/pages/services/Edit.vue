<template>
    <div class="columns is-centered">
        <div class="column is-three-quarters-desktop is-full-touch">
            <enso-form class="box form-box"
                @ready="form = $event.form">
                <template #suppliers>
                    <div class="wrapper is-block">
                        <div class="columns">
                            <div class="column is-6-tablet">
                                <form-field :field="form.field('suppliers')"
                                    :custom-params="$route.params"/>
                            </div>
                        </div>
                        <supplier v-for="supplier in form.field('suppliers').value"
                            :key="supplier.id"
                            :supplier="supplier"
                            :errors="form.errors"
                            @acquisition-price-updated="supplier.cost.acquisitionPrice = $event"/>
                    </div>
                </template>
            </enso-form>
        </div>
    </div>
</template>

<script setup>
import { EnsoForm, FormField } from '@enso-ui/forms/bulma';
import { ref } from 'vue';
import Supplier from './components/Supplier.vue';

const form = ref(null);

</script>
