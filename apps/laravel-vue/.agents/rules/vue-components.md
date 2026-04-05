# Vue 3 & Inertia Components

## 1. Composition API Support
Always use Vue 3 `<script setup lang="ts">`. NEVER use the Options API (`export default { data() {} }`).

```vue
<!-- ✅ GOOD -->
<script setup lang="ts">
import { ref } from 'vue';
import { useForm } from '@inertiajs/vue3';

const props = defineProps<{ user: User }>();

const form = useForm({
  name: props.user.name,
});

const submit = () => {
    form.put(route('users.update', props.user.id));
};
</script>

<template>
  <form @submit.prevent="submit">
      <input v-model="form.name" />
      <button :disabled="form.processing">Save</button>
  </form>
</template>
```

## 2. Inertia `useForm`
For form submissions, ALWAYS use Inertia's `useForm` helper to handle forms, loading states, and validation errors automatically. Avoid generic Axios/Fetch POST calls for page navigations.

## 3. Link tags
NEVER use `<a href="...">` for internal routing. ALWAYS use the `<Link>` component from `@inertiajs/vue3` to prevent full page reloads.

## 4. Ziggy Routes
Always use the `route('route.name')` helper provided by Ziggy instead of hardcoding URLs (`/users/1/edit`).
