<template>
    <div>
        <div class="mt-8 sm:mx-auto sm:w-full sm:max-w-md">
            <div class="bg-white py-8 px-4 shadow sm:rounded-lg sm:px-10">
                <form class="space-y-6" @submit.prevent="login">
                    <!-- email address field -->
                    <v-input v-model="state.form.email" :v="v$.email" label="Email Address" type="email" />

                    <!-- password field -->
                    <v-input v-model="state.form.password" :v="v$.password" label="Password" type="password" />
                    <nuxt-link class="block font-semibold text-emerald-800" to="/forgot-password">Forgot Password?
                    </nuxt-link>

                    <div>
                        <button type="submit"
                            class="w-full py-2 px-4 font-normal text-sm rounded-md shadow-md text-white bg-emerald-800 hover:bg-emerald-900">
                            Sign in
                        </button>
                    </div>
                </form>
            </div>
        </div>
    </div>
</template>
<script lang="ts">
import useVuelidate, {
    required,
    email,
} from '../utlis/vuelidate/useVuelidate';

export default {
    name: 'LoginPage',
};
</script>

<script lang="ts" setup>

const state = reactive({
    form: {
        email: '',
        password: '',
    },
});

/**
 * validation rules
 */
const rules = {
    email: { required, email },
    password: { required },
};
const v$ = useVuelidate(rules, state.form);

/**
 * login
 *
 * @returns {Promise<void>}
 */
async function login(): Promise<void> {
    const isFormCorrect = await v$.value.$validate();
    if (!isFormCorrect) {
        // Show error messages
        return;
    }

    const payload = { ...state.form };
    // Call API with payload
}
</script>