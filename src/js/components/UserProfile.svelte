<script>
  import InlineField from "./InlineField.svelte";
  import { useInlineEdit } from "./useInlineEdit.svelte";

  const user = {
    name: "Jane Doe",
    email: "jane@example.com",
    bio: "Frontend developer who loves Svelte.",
  };

  async function saveProfile(updated) {
    await new Promise((r) => setTimeout(r, 500));
    Object.assign(user, updated)
    console.log(user)
  }

  const edit = useInlineEdit(user, saveProfile);
</script>

<div class="inline-fields">
  <InlineField label="Name" bind:value={edit.draft.name} />
  <InlineField label="Email" type="email" bind:value={edit.draft.email} />
  <InlineField label="Bio" type="textarea" bind:value={edit.draft.bio} />
</div>

{#if edit.isDirty()}
  <button onclick={edit.save}>Save</button>
  <button onclick={edit.cancel}>Cancel</button>
{/if}

<style>
    .inline-fields {
        display: flex;
        flex-direction: column;
        justify-content: space-between;
        gap: 20px;
    }

    button {
        width: 80px;
        margin-top: 10px;
    }
</style>
