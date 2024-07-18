<script context="module">    
    import { createClient } from '@supabase/supabase-js';  
    
    const SUPABASE_URL = 'https://vhjdmjrluctpaljlzggc.supabase.co';
    const SUPABASE_ANON_KEY = '';    
    const supabase = createClient(SUPABASE_URL, SUPABASE_ANON_KEY);
  </script>
  
  <script lang="ts">    
    import { onMount } from 'svelte';  
    
    type Fees = {
      vehicle_type: String;
      effective_date: Date;
      daily_rate: Number;
      discount: Number;
      gst: Number;
      excess: Number;
      excess_removal: Number;
      relocation: Number;
    };  
    
    export let m_fees: Fees[] = [];
  
    onMount(async () => {
      try {        
        const { data, error } = await supabase
          .from('m_fees') 
          .select('vehicle_type, effective_date, daily_rate, discount, gst, excess, excess_removal, relocation');         
        
        if (error) {
          throw new Error(`Error fetching data: ${error.message}`);
        }  
        m_fees = data ?? [];        
      
      } catch (error) {        
        console.error(error);
      }
    });
  </script>
  
  <h1>Fees</h1>    
  
  {#if m_fees.length > 0}
    <table>
      <thead>        
        <tr>
          <th>Vehicle Type</th>
          <th>Effective Date</th>
          <th>Daily Rate</th>
          <th>Discount</th>
          <th>GST</th>
          <th>Excess</th>
          <th>Excess Removal</th>
          <th>Relocation</th>
        </tr>
      </thead>
      <tbody>        
        {#each m_fees as fees}
          <tr>
            <td>{fees.vehicle_type}</td>
            <td>{fees.effective_date}</td>
            <td>{fees.daily_rate}</td>
            <td>{fees.discount}</td>
            <td>{fees.gst}</td>
            <td>{fees.excess}</td>
            <td>{fees.excess_removal}</td>
            <td>{fees.relocation}</td>
          </tr>         
        {/each}
      </tbody>
    </table>
  {:else}
    <p>Fetching data...</p>
  {/if}
  