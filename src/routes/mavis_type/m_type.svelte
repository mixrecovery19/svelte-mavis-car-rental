<script context="module">
    import { createClient } from '@supabase/supabase-js';
 
 const SUPABASE_URL = 'https://vhjdmjrluctpaljlzggc.supabase.co';
 const SUPABASE_ANON_KEY = '';

 const supabase = createClient(SUPABASE_URL, SUPABASE_ANON_KEY);
</script>

<script lang="ts">    
 import { onMount } from 'svelte';  

 type Type = {
   vehicle_type: String;
   make: String;
   model: String;
   year: Number;
   seating_cap: Number;
   body_style: String;
   engine_cap: Number; 
     };
   
 export let m_type: Type[] = [];

 onMount(async () => {
   try {        
     const { data, error } = await supabase
       .from('m_type') // table name
       .select('vehicle_type, make, model, year, seating_cap, body_style, engine_cap'); // column name(s)        
     
     if (error) {
       throw new Error(`Error fetching data: ${error.message}`);
     } 
    m_type = data ?? []; // Explanation of ??: In JavaScript and TypeScript, the ?? operator is called the "nullish coalescing operator." It provides a way to handle default values when dealing with 'null' or 'undefined' values. 
           
   } catch (error) {
     console.error(error);
   }
 });
</script>

<h1>Type</h1> 

{#if m_type.length > 0}
 <table>
   <thead>        
     <tr>
       <th>Vehicle Type</th>
       <th>Make</th>  
       <th>Model</th>
       <th>Year</th>
       <th>Seating Capacity</th>
       <th>Body Style</th>
       <th>Engine Capacity</th>
     </tr>
   </thead>
   <tbody>        
     {#each m_type as type}
       <tr>
         <td>{type.vehicle_type}</td>
         <td>{type.make}</td>
         <td>{type.model}</td> 
         <td>{type.year}</td> 
         <td>{type.seating_cap}</td>
         <td>{type.body_style}</td>
         <td>{type.engine_cap}</td>          
       </tr>         
     {/each}
   </tbody>
 </table>
{:else}
 <p>Fetching data...</p>
{/if}
