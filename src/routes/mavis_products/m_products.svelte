<script context="module">
       import { createClient } from '@supabase/supabase-js';
    
    const SUPABASE_URL = 'https://vhjdmjrluctpaljlzggc.supabase.co';
    const SUPABASE_ANON_KEY = '';
   
    const supabase = createClient(SUPABASE_URL, SUPABASE_ANON_KEY);
  </script>
  
  <script lang="ts">    
    import { onMount } from 'svelte';  
   
    type Products = {
      product_no: String;
      product_name: String;
      product_description: String;
      plant_id: String;
      finished_product_parts_id: String;
      qty_on_hand: String;      
        };
      
    export let m_products: Products[] = [];
  
    onMount(async () => {
      try {        
        const { data, error } = await supabase
          .from('m_products') 
          .select('product_no, product_name, product_description, plant_id, finished_product_parts_id, qty_on_hand');         
        
        if (error) {
          throw new Error(`Error fetching data: ${error.message}`);
        } 
       m_products = data ?? []; 
      }
       catch (error) {
        console.error(error);
      }
    });
  </script>
  
  <h1>Products</h1> 
  
  {#if m_products.length > 0}
    <table>
      <thead>        
        <tr>
          <th>Product No.</th>
          <th>Product Name</th>
          <th>Product Description</th>
          <th>Plant ID</th>
          <th>Finished Product Parts ID</th>
          <th>QTY On Hand</th>                    
        </tr>
      </thead>
      <tbody>        
        {#each m_products as products}
          <tr>
            <td>{products.product_no}</td>
            <td>{products.product_name}</td>
            <td>{products.product_description}</td>
            <td>{products.plant_id}</td> 
            <td>{products.finished_product_parts_id}</td> 
            <td>{products.qty_on_hand}</td>                
          </tr>         
        {/each}
      </tbody>
    </table>
  {:else}
    <p>Fetching data...</p>
  {/if}
  