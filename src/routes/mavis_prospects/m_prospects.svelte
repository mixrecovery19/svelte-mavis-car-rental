<script context="module">
    import { createClient } from '@supabase/supabase-js';
 
 const SUPABASE_URL = 'https://vhjdmjrluctpaljlzggc.supabase.co';
 const SUPABASE_ANON_KEY = '';

 const supabase = createClient(SUPABASE_URL, SUPABASE_ANON_KEY);
</script>

<script lang="ts">    
 import { onMount } from 'svelte';  

 type Prospects = {
   customer_no: Number;
   surname: String;
   first_name: String;
   street_no: String;
   street: String;
   suburb: String;
   state: String;
   post_code: String;
     };
   
 export let m_prospects: Prospects[] = [];

 onMount(async () => {
   try {        
     const { data, error } = await supabase
       .from('m_prospects') 
       .select('customer_no, surname, first_name, street_no, street, suburb, state, post_code');       
     
     if (error) {
       throw new Error(`Error fetching data: ${error.message}`);
     } 
    m_prospects = data ?? [];
           
   } catch (error) {
     console.error(error);
   }
 });
</script>

<h1>Prospects</h1> 

{#if m_prospects.length > 0}
 <table>
   <thead>        
     <tr>
       <th>Customer No.</th>
       <th>Surname</th> 
       <th>First Name</th>  
       <th>Street No.</th>  
       <th>Street</th>   
       <th>Suburb</th>  
       <th>State</th>
       <th>Post Code</th>     
     </tr>
   </thead>
   <tbody>        
     {#each m_prospects as prospects}
       <tr>
         <td>{prospects.customer_no}</td>
         <td>{prospects.surname}</td>
         <td>{prospects.first_name}</td>
         <td>{prospects.street_no}</td> 
         <td>{prospects.street}</td> 
         <td>{prospects.suburb}</td> 
         <td>{prospects.state}</td>  
         <td>{prospects.post_code}</td>             
       </tr>         
     {/each}
   </tbody>
 </table>
{:else}
 <p>Fetching data...</p>
{/if}
