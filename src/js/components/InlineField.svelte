<script lang="ts">
  let {
    label,
    value = $bindable(),
    type = "text"
  } = $props();

  let isEditing = $state(false);
  let originalValue = value;

  function startEdit() {
    isEditing = true;
    originalValue = value;
  }

  function commitEdit() {
    isEditing = false
  }

  function cancelEdit() {
    isEditing = false;
    value = originalValue
  }

  function handleKeydown(e: KeyboardEvent) {
    if (e.key === "Enter" && type !== "textarea") {
        e.preventDefault();
        commitEdit();
    }

    if (e.key === "Escape") {
        e.preventDefault()
        cancelEdit()
    }
  }
</script>

<div class="form-group">
  <div class="label">{label}</div>
  {#if isEditing}
    {#if type === "textarea"}
      <textarea autofocus aria-label={label} bind:value onblur={commitEdit} onkeydown={handleKeydown} ></textarea>
    {:else}
      <input autofocus aria-label={label} bind:value {type} onblur={commitEdit} onkeydown={handleKeydown} />
    {/if}
  {:else}
    <button type="button" aria-label={`Edit ${label}`} class="value" onclick={startEdit}>{value}</button>
  {/if}
</div>

<style>
    .form-group {
        display: flex;
        flex-direction: row;
        gap: 20px;
        /* justify-content: space-between; */
    }

    .value {
        cursor: pointer;
        padding: 5px;
    }

    .value:hover {
        background: rosybrown;
    }
</style>
