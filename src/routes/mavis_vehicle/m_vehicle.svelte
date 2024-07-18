<script context="module">
    import { createClient } from '@supabase/supabase-js';
 
 const SUPABASE_URL = 'https://vhjdmjrluctpaljlzggc.supabase.co';
 const SUPABASE_ANON_KEY = '';

 const supabase = createClient(SUPABASE_URL, SUPABASE_ANON_KEY);
</script>

<script lang="ts">    
 import { onMount } from 'svelte';  

 type Vehicle = {
   rego_no: String;
   vehicle_type: String;
   branch_code: String;
   color: String;
   transmission: String;
   purchased: Date;
   location: String;
     };
   
 export let m_vehicle: Vehicle[] = [];

 onMount(async () => {
   try {        
     const { data, error } = await supabase
       .from('m_vehicle') 
       .select('rego_no, vehicle_type, branch_code, color, transmission, purchased, location');       
     
     if (error) {
       throw new Error(`Error fetching data: ${error.message}`);
     } 
    m_vehicle = data ?? [];  
           
   } catch (error) {
     console.error(error);
   }
 });
</script>

<h1>Vehicle</h1> 

{#if m_vehicle.length > 0}
 <table>
   <thead>        
     <tr>
       <th>Rego No.</th>
       <th>Vehicle Type</th>
       <th>Branch Code</th>  
       <th>Color</th>
       <th>Transmission</th>
       <th>Purchased</th>
       <th>Location</th>
     </tr>
   </thead>
   <tbody>        
     {#each m_vehicle as vehicle}
       <tr>
         <td>{vehicle.rego_no}</td>
         <td>{vehicle.vehicle_type}</td>
         <td>{vehicle.branch_code}</td> 
         <td>{vehicle.color}</td>  
         <td>{vehicle.transmission}</td>
         <td>{vehicle.purchased}</td>  
         <td>{vehicle.location}</td>    
       </tr>         
     {/each}
   </tbody>
 </table>
{:else}
 <p>Fetching data...</p>
{/if}
