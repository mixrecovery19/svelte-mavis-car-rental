<script context="module">    
    import { createClient } from '@supabase/supabase-js';  
    
    const SUPABASE_URL = 'https://vhjdmjrluctpaljlzggc.supabase.co';
    const SUPABASE_ANON_KEY = 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6InZoamRtanJsdWN0cGFsamx6Z2djIiwicm9sZSI6InNlcnZpY2Vfcm9sZSIsImlhdCI6MTcwODQ3MTExNCwiZXhwIjoyMDI0MDQ3MTE0fQ.qNv63B0HVFo3ah516mUwqzJzxOjzgksyb3gjOEEFALg';    
    const supabase = createClient(SUPABASE_URL, SUPABASE_ANON_KEY);
  </script>
  
  <script lang="ts">    
    import { onMount } from 'svelte';  
    
    type Parts = {
      part_no: String;
      part_description: String;
      plant_parts_id: String;
      finished_product_parts_id: String;
      in_stock: Number;
      cost_price: Number;
      supplier_id: String;
      
    };  
    
    export let m_parts: Parts[] = [];
  
    onMount(async () => {
      try {        
        const { data, error } = await supabase
          .from('m_parts') 
          .select('part_no, part_description, plant_parts_id, finished_product_parts_id, in_stock, cost_price, supplier_id');         
        
        if (error) {
          throw new Error(`Error fetching data: ${error.message}`);
        }  
        
        m_parts = data ?? [];         
      
      } catch (error) {        
        console.error(error);
      }
    });
  </script>
  
  <h1>Parts</h1>    
 
  {#if m_parts.length > 0}
    <table>
      <thead>        
        <tr>
          <th>Part No.</th>
          <th>Part Description</th>
          <th>Plant Parts ID</th>
          <th>Finished Product Parts ID</th>
          <th>In Stock</th>
          <th>Cost Price</th>
          <th>Supplier ID</th>
        </tr>
      </thead>
      <tbody>       
        {#each m_parts as parts}
          <tr>
            <td>{parts.part_no}</td>
            <td>{parts.part_description}</td>
            <td>{parts.plant_parts_id}</td>
            <td>{parts.finished_product_parts_id}</td>
            <td>{parts.in_stock}</td>
            <td>{parts.cost_price}</td>
            <td>{parts.supplier_id}</td>
          </tr>         
        {/each}
      </tbody>
    </table>
  {:else}
    <p>Fetching data...</p>
  {/if}
  