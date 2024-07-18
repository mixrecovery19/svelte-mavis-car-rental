<script context="module">
    import { createClient } from '@supabase/supabase-js';
 
 const SUPABASE_URL = 'https://vhjdmjrluctpaljlzggc.supabase.co';
 const SUPABASE_ANON_KEY = '';

 const supabase = createClient(SUPABASE_URL, SUPABASE_ANON_KEY);
</script>

<script lang="ts">    
 import { onMount } from 'svelte';  

 type Rental = {
   rental_no: Number;
   cust_id: Number;
   rego_no: String;
   start_klm: Number;
   start_date: Date;
   finish_klm: Number;
   returned: Date;
   petrol_$: Number;
   relocation_$: Number;
   gross_hire_$: Number;
   discount_$: Number;
   discount_option: String;
   gst_$: Number;
   insurance_$: Number;
   insurance_option: String;
   date_due: Date;
   return_location: String;
     };
   
 export let m_rental: Rental[] = [];

 onMount(async () => {
   try {        
     const { data, error } = await supabase
       .from('m_rental') 
       .select('rental_no, cust_id, rego_no, start_klm, start_date, finish_klm, returned, petrol_$, relocation_$, gross_hire_$, discount_$, discount_option, gst_$, insurance_$, insurance_option, date_due, return_location');        
     
     if (error) {
       throw new Error(`Error fetching data: ${error.message}`);
     } 
    m_rental = data ?? []; 
           
   } catch (error) {
     console.error(error);
   }
 });
</script>

<h1>Rental</h1> 

{#if m_rental.length > 0}
 <table>
   <thead>        
     <tr>
       <th>Rental No.</th>
       <th>Customer ID</th> 
       <th>Rego No.</th>  
       <th>Start Klm</th>  
       <th>Start Date</th>   
       <th>Finish Klm</th>  
       <th>Returned</th>
       <th>Petrol $</th>     
       <th>Relocation $</th>
       <th>Gross Hire $</th>
       <th>Discount $</th>
       <th>Discount Option</th>
       <th>GST</th>
       <th>Insurance $</th>
       <th>Insurance Option</th>
       <th>Date Due</th>
       <th>Return Location</th>
     </tr>
   </thead>
   <tbody>        
     {#each m_rental as rental}
       <tr>
         <td>{rental.rental_no}</td>
         <td>{rental.cust_id}</td> 
         <td>{rental.rego_no}</td>  
         <td>{rental.start_klm}</td> 
         <td>{rental.start_date}</td> 
         <td>{rental.finish_klm}</td>  
         <td>{rental.returned}</td>  
         <td>{rental.petrol_$}</td>  
         <td>{rental.relocation_$}</td>
         <td>{rental.gross_hire_$}</td>
         <td>{rental.discount_$}</td>
         <td>{rental.discount_option}</td>
         <td>{rental.gst_$}</td>
         <td>{rental.insurance_$}</td>
         <td>{rental.insurance_option}</td>
         <td>{rental.date_due}</td>
         <td>{rental.return_location}</td>
       </tr>         
     {/each}
   </tbody>
 </table>
{:else}
 <p>Fetching data...</p>
{/if}
