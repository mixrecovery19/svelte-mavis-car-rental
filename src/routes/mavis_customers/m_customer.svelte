<script context="module">    
    import { createClient } from '@supabase/supabase-js';  
    
    const SUPABASE_URL = 'https://vhjdmjrluctpaljlzggc.supabase.co';
    const SUPABASE_ANON_KEY = '';    
    const supabase = createClient(SUPABASE_URL, SUPABASE_ANON_KEY);
  </script>
  
  <script lang="ts">    
    import { onMount } from 'svelte';  
   
    type Customer = {
      cust_id: Number;
      first_name: String;
      last_name: String;
      company: String;
      street_no: String;
      street_name: String;
      suburb: String;
      state: String;
      post_code: Number;
      phone: Number;
      license_no: String;


    };      
    export let m_customer: Customer[] = [];
  
    onMount(async () => {
      try {       
        const { data, error } = await supabase
          .from('m_customer') 
          .select('cust_id, first_name, last_name, company, street_no, street_name, suburb, state, post_code, phone, license_no');         
        
        if (error) {
          throw new Error(`Error fetching data: ${error.message}`);
        }        
        m_customer = data ?? [];   
      } 
        catch (error) {        
        console.error(error);
      }      
    });
  </script>
  
  <h1>All Users</h1>   
 
  {#if m_customer.length > 0}
    <table>
      <thead>        
        <tr>
          <th>Customer I.D.</th>
          <th>First Name</th>
          <th>Last Name</th>
          <th>Company</th>
          <th>Street No.</th>
          <th>Street Name</th>
          <th>Suburb</th>
          <th>State</th>
          <th>Postcode</th>
          <th>Phone No.</th>
          <th>License No.</th>
        </tr>
      </thead>
      <tbody>
        
        {#each m_customer as customer}
          <tr>
            <td>{customer.cust_id}</td>
            <td>{customer.first_name}</td>
            <td>{customer.last_name}</td>
            <td>{customer.company}</td>
            <td>{customer.street_no}</td>
            <td>{customer.street_name}</td>
            <td>{customer.suburb}</td>
            <td>{customer.state}</td>
            <td>{customer.post_code}</td>
            <td>{customer.phone}</td>
            <td>{customer.license_no}</td>
          </tr>
        {/each}
      </tbody>
    </table>
  {:else}
    <p>Fetching data...</p>
  {/if}
  