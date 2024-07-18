<script context="module">    
    import { createClient } from '@supabase/supabase-js';  
    
    const SUPABASE_URL = 'https://vhjdmjrluctpaljlzggc.supabase.co';
    const SUPABASE_ANON_KEY = '';    
    const supabase = createClient(SUPABASE_URL, SUPABASE_ANON_KEY);
  </script>
  
  <script lang="ts">    
    import { onMount } from 'svelte';  
   
    type Plants = {
      plant_id: String;
      plant_name: String;
      plant_street_no: String;
      plant_street: String;
      plant_suburb: String;
      plant_state: String;
      plant_country: String;
      plant_postcode: String;
      plant_phone: String;
      plant_email: String;
      product_no: String;
        };  
    
    export let m_plants: Plants[] = [];
  
    onMount(async () => {
      try {        
        const { data, error } = await supabase
          .from('m_plants') 
          .select('plant_id, plant_name, plant_street_no, plant_street, plant_suburb, plant_state, plant_country, plant_postcode, plant_phone, plant_email, product_no');
                
        if (error) {
          throw new Error(`Error fetching data: ${error.message}`);
        }          
        m_plants = data ?? [];        
      
      } catch (error) {        
        console.error(error);
      }
    });
  </script>
  
  <h1>Plant Parts</h1>    
  
  {#if m_plants.length > 0}
    <table>
      <thead>        
        <tr>
          <th>Plant ID</th>
          <th>Plant Name</th>
          <th>Plant Street No.</th>
          <th>Plant Street</th> 
          <th>Plant Suburb</th>  
          <th>Plant State</th>
          <th>Plant Country</th>
          <th>Plant Postcode</th> 
          <th>Plant Phone</th>   
          <th>Plant Email</th>
          <th>Product No.</th>          
        </tr>
      </thead>
      <tbody>
        
        {#each m_plants as plants}
          <tr>
            <td>{plants.plant_id}</td>
            <td>{plants.plant_name}</td>
            <td>{plants.plant_street_no}</td>
            <td>{plants.plant_street}</td> 
            <td>{plants.plant_suburb}</td> 
            <td>{plants.plant_state}</td>
            <td>{plants.plant_country}</td> 
            <td>{plants.plant_postcode}</td>
            <td>{plants.plant_phone}</td> 
            <td>{plants.plant_email}</td>  
            <td>{plants.product_no}</td>           
          </tr>         
        {/each}
      </tbody>
    </table>
  {:else}
    <p>Fetching data...</p>
  {/if}
  