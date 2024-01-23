<script setup lang="ts">
import { useForm } from "vee-validate";
import { toTypedSchema } from "@vee-validate/zod";
import { z } from "zod";

const schema = z.object({
  name: z.preprocess((val) => (val ? val : undefined), z.string().optional()),
});

const { defineField, handleSubmit } = useForm({
  validationSchema: toTypedSchema(schema),
});

// name is Ref<unknown> here?
const [name, nameProps] = defineField("name");

console.log(nameProps);

const onSubmit = handleSubmit((form) => {
  // form.name is string | undefined here.
  console.log(form.name);
});
</script>

<template>
  <form @submit="onSubmit">
    <div>
      <input type="text" v-model="name" />
    </div>

    <button type="submit">Submit</button>
  </form>
</template>
