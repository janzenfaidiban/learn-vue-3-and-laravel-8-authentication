<template>    
    <form class="form-signin" @submit.prevent="submit">
        <h1 class="h3 mb-3 fw-normal">Please reet your password</h1>

            <input v-model="password" type="password" class="form-control" placeholder="Password" required>

            <input v-model="passwordConfirm" type="password" class="form-control" placeholder="Password Confirm" required>

            <button class="w-100 btn btn-lg btn-primary" type="submit">Submit</button>
    </form>
</template>

<script>
    import {ref} from 'vue';
    import axios from 'axios';
    import {useRoute, useRouter} from 'vue-router';

    export default {
        name: 'Reset',
        setup() {
            const password = ref('');
            const passwordConfirm = ref('');
            const route = useRoute();
            const router = useRouter();

            const submit = async () => {
                await axios.post('reset', {
                    token: route.params.token,
                    password: password.value,
                    password_confirm: passwordConfirm.value
                });

                await router.push('/login');
            }

            return {
                password,
                passwordConfirm,
                submit
            }
        }
    }
</script>