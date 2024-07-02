<script context="module">    
    import { createClient } from '@supabase/supabase-js';  
    
    const SUPABASE_URL = 'https://vhjdmjrluctpaljlzggc.supabase.co';
    const SUPABASE_ANON_KEY = 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6InZoamRtanJsdWN0cGFsamx6Z2djIiwicm9sZSI6InNlcnZpY2Vfcm9sZSIsImlhdCI6MTcwODQ3MTExNCwiZXhwIjoyMDI0MDQ3MTE0fQ.qNv63B0HVFo3ah516mUwqzJzxOjzgksyb3gjOEEFALg';    
    const supabase = createClient(SUPABASE_URL, SUPABASE_ANON_KEY);
  </script>
  
  <script lang="ts">    
    import { onMount } from 'svelte';  
    
    type Branch = {
      branch_code: String;
      manager: String;
      branch_address: String;
      suburb: String;
      state: String;
      post_code: Number;
      phone: String;
      fax: String;
      branch_name: String;

    };  
    
    export let m_branch: Branch[] = [];
  
    onMount(async () => {
      try {        
        const { data, error } = await supabase
          .from('m_branch')
          .select('branch_code, manager, branch_address, suburb, state, post_code, phone, fax, branch_name');         
        
        if (error) {
          throw new Error(`Error fetching data: ${error.message}`);
        }  
        
        m_branch = data ?? [];         
      
      } catch (error) {       
        console.error(error);
      }
    });
  </script>
  
  <h1>Branches</h1>  

  {#if m_branch.length > 0}
    <table>
      <thead>        
        <tr>
          <th>Branch Code</th>
          <th>Manager</th>
          <th>Branch Address</th>
          <th>Suburb</th>
          <th>State</th>
          <th>Post Code</th>
          <th>Phone</th>
          <th>Fax</th>
          <th>Branch Name</th>
        </tr>
      </thead>
      <tbody>
        
        {#each m_branch as branch}
          <tr>
            <td>{branch.branch_code}</td>
            <td>{branch.manager}</td>
            <td>{branch.branch_address}</td>
            <td>{branch.suburb}</td>
            <td>{branch.state}</td>
            <td>{branch.post_code}</td>
            <td>{branch.phone}</td>
            <td>{branch.fax}</td>
            <td>{branch.branch_name}</td>
          </tr>         
        {/each}
      </tbody>
    </table>
  {:else}
    <p>Fetching data...</p>
  {/if}
  