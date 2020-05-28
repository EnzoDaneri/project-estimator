<script>
  import { createEventDispatcher } from 'svelte';
  import materialStore from './material-store.js';

  const dispatch = createEventDispatcher();
  let materials = [];

 materialStore.subscribe(items => {
     materials = items;
//cada vez que se actualice, materials será = items
 })


$: total = materials.reduce((prev, next) => {
     prev += next.price;
     return prev;
}, 0);



const edit = (id, name, price ) => {
      dispatch('edit', {id, name, price});
}



// $: console.log(materials);

const formatter = new Intl.NumberFormat('en-US', {
    style: 'currency',
    currency: 'USD'
})

</script>

<h1>{total}</h1>
<table class="primary">
 <thead>
   <tr>
     <th>Material</th>
     <th>Price</th>
     <th></th>
   
   </tr>
 </thead>
 <tbody>
 {#each materials as material (material.id)}
  <tr on:click={edit(material.id, material.name, material.price)}>
    <td>{material.name}</td>
    <td>{formatter.format( material.price)}</td>
    <td><i class="far fa-trash-alt"></i> </td>
  </tr>
 {/each}
  <tr>
    <td>Total</td>
    <td colspan="2">{formatter.format(total)}</td>
  </tr>
 </tbody>
</table>


<style>
table {
    width: 100%;
}

tr {
    cursor: pointer;
}

</style>