<script context="module">    
    import { createClient } from '@supabase/supabase-js';  
    
    const SUPABASE_URL = 'https://vhjdmjrluctpaljlzggc.supabase.co';
    const SUPABASE_ANON_KEY = 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6InZoamRtanJsdWN0cGFsamx6Z2djIiwicm9sZSI6InNlcnZpY2Vfcm9sZSIsImlhdCI6MTcwODQ3MTExNCwiZXhwIjoyMDI0MDQ3MTE0fQ.qNv63B0HVFo3ah516mUwqzJzxOjzgksyb3gjOEEFALg';    
    const supabase = createClient(SUPABASE_URL, SUPABASE_ANON_KEY);
  </script>

  <script lang="ts">
    
    import { onMount } from 'svelte';  

    type PlantParts = {
      plant_parts_id: String;
      part_no: String;
      plant_id: Number;
      dispatched: Date;      
        };  
    
    export let m_plant_parts: PlantParts[] = [];

    onMount(async () => {
      try {        
        const { data, error } = await supabase
          .from('m_plant_parts') 
          .select('plant_parts_id, part_no, plant_id, dispatched');         
        
        if (error) {
          throw new Error(`Error fetching data: ${error.message}`);
        }  
        
        m_plant_parts = data ?? [];          
      
      } catch (error) {        
        console.error(error);
      }
    });
  </script>
  
  <h1>Plant Parts</h1>    
  
  {#if m_plant_parts.length > 0}
    <table>
      <thead>        
        <tr>
          <th>Plant Parts ID</th>
          <th>Part No.</th>
          <th>Plant ID</th>
          <th>Dispatched</th>                 
        </tr>
      </thead>
      <tbody>        
        {#each m_plant_parts as plantparts}
          <tr>
            <td>{plantparts.plant_parts_id}</td>
            <td>{plantparts.part_no}</td>
            <td>{plantparts.plant_id}</td>
            <td>{plantparts.dispatched}</td>                 
          </tr>         
        {/each}
      </tbody>
    </table>
  {:else}
    <p>Fetching data...</p>
  {/if}
  