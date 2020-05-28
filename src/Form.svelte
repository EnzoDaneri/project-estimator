<script>

export let id;
export let name= '';
export let price;


$: mode = id ? 'edit' : 'add'; 
$: canSubmit = price >=0 && name !== '';

const submit = () => {
    if(!canSubmit) {
        return;
    }
   price = '';
   name= '';
   id= undefined;
}

const cancel= () => {
   price = '';
   name= '';
   id= undefined;
}

</script>



<form on:submit|preventDefault={submit}>
<fieldset>
 <label for="nameField">Material</label>
 <input bind:value={name} type="text" id="nameField"
 placeholder="wood, glue, etc">

  <label for="priceField">Price</label>
 <input bind:value={price} type="number" id="priceField" min="0" step="any"
 placeholder="Price">

</fieldset>
<button disabled={!canSubmit} type="submit" class="float-right">{mode}</button>

{#if mode === 'edit'}
<button on:click={cancel} type="button" class="float-right">Cancel</button>
{/if}
</form>


<style>
button {
    margin-left: 20px;
}
button:disabled {
    cursor: not-allowed;
}

</style>