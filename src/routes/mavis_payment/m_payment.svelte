<script context="module">    
    import { createClient } from '@supabase/supabase-js';  
    
    const SUPABASE_URL = 'https://vhjdmjrluctpaljlzggc.supabase.co';
    const SUPABASE_ANON_KEY = '';    
    const supabase = createClient(SUPABASE_URL, SUPABASE_ANON_KEY);
  </script>
  
  <script lang="ts">    
    import { onMount } from 'svelte';  
    
    type Payment = {
      payment_no: Number;
      rental_no: Number;
      payment_date: Date;
      payment_type: String;
      reference_no: String;
      expiry_date: String;
      amount: Number;
        };  
    
    export let m_payment: Payment[] = [];
  
    onMount(async () => {
      try {        
        const { data, error } = await supabase
          .from('m_payment') 
          .select('payment_no, rental_no, payment_date, payment_type, reference_no, expiry_date, amount');        
        
        if (error) {
          throw new Error(`Error fetching data: ${error.message}`);
        }  
        
        m_payment = data ?? [];         
      
      } catch (error) {        
        console.error(error);
      }
    });
  </script>
  
  <h1>Payment</h1>    
  
  {#if m_payment.length > 0}
    <table>
      <thead>        
        <tr>
          <th>Payment No.</th>
          <th>Rental No.</th>
          <th>Payment Date</th>
          <th>Payment Type</th>
          <th>Reference No.</th>
          <th>Expiry Date</th>
          <th>Amount</th>          
        </tr>
      </thead>
      <tbody>
        
        {#each m_payment as payment}
          <tr>
            <td>{payment.payment_no}</td>
            <td>{payment.rental_no}</td>
            <td>{payment.payment_date}</td>
            <td>{payment.payment_type}</td>
            <td>{payment.reference_no}</td>
            <td>{payment.expiry_date}</td>
            <td>{payment.amount}</td>            
          </tr>         
        {/each}
      </tbody>
    </table>
  {:else}
    <p>Fetching data...</p>
  {/if}
  