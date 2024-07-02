<script context="module">    
    import { createClient } from '@supabase/supabase-js';  
    
    const SUPABASE_URL = 'https://vhjdmjrluctpaljlzggc.supabase.co';
    const SUPABASE_ANON_KEY = 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6InZoamRtanJsdWN0cGFsamx6Z2djIiwicm9sZSI6InNlcnZpY2Vfcm9sZSIsImlhdCI6MTcwODQ3MTExNCwiZXhwIjoyMDI0MDQ3MTE0fQ.qNv63B0HVFo3ah516mUwqzJzxOjzgksyb3gjOEEFALg';    
    const supabase = createClient(SUPABASE_URL, SUPABASE_ANON_KEY);
  </script>
  
  <script lang="ts">    
    import { onMount } from 'svelte'; 
    
    type FinishedProductParts = {
      finished_product_parts_id: String;
      part_no: String;
      product_no: String;
      
    };  
    
    export let m_finished_product_parts: FinishedProductParts[] = [];
  
    onMount(async () => {
      try {        
        const { data, error } = await supabase
          .from('m_finished_product_parts') 
          .select('finished_product_parts_id, part_no, product_no');         
        
        if (error) {
          throw new Error(`Error fetching data: ${error.message}`);
        } 
        
        m_finished_product_parts = data ?? [];         
      
      } catch (error) {        
        console.error(error);
      }
    });
  </script>
  
  <h1>Finished Product Parts</h1>    
 
  {#if m_finished_product_parts.length > 0}
    <table>
      <thead>        
        <tr>
          <th>Finished Product Parts ID</th>
          <th>Part No.</th>
          <th>Product No.</th>
        </tr>
      </thead>
      <tbody>
       
        {#each m_finished_product_parts as finishedproductparts}
          <tr>
            <td>{finishedproductparts.finished_product_parts_id}</td>
            <td>{finishedproductparts.part_no}</td>
            <td>{finishedproductparts.product_no}</td>
          </tr>         
        {/each}
      </tbody>
    </table>
  {:else}
    <p>Fetching data...</p>
  {/if}
  