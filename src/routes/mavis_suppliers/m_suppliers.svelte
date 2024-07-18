<script context="module">
    import { createClient } from '@supabase/supabase-js';
 
 const SUPABASE_URL = 'https://vhjdmjrluctpaljlzggc.supabase.co';
 const SUPABASE_ANON_KEY = '';

 const supabase = createClient(SUPABASE_URL, SUPABASE_ANON_KEY);
</script>

<script lang="ts">    
 import { onMount } from 'svelte';  

 type Suppliers = {
   supplier_id: String;
   supplier_name: String;
   part_no: String;
     };
   
 export let m_suppliers: Suppliers[] = [];

 onMount(async () => {
   try {        
     const { data, error } = await supabase
       .from('m_suppliers')
       .select('supplier_id, supplier_name, part_no');       
     
     if (error) {
       throw new Error(`Error fetching data: ${error.message}`);
     } 
    m_suppliers = data ?? []; 
           
   } catch (error) {
     console.error(error);
   }
 });
</script>

<h1>Suppliers</h1> 

{#if m_suppliers.length > 0}
 <table>
   <thead>        
     <tr>
       <th>Supplier ID</th>
       <th>Supplier Name</th>
       <th>Part No.</th>  
     </tr>
   </thead>
   <tbody>        
     {#each m_suppliers as suppliers}
       <tr>
         <td>{suppliers.supplier_id}</td>
         <td>{suppliers.supplier_name}</td>
         <td>{suppliers.part_no}</td>            
       </tr>         
     {/each}
   </tbody>
 </table>
{:else}
 <p>Fetching data...</p>
{/if}
