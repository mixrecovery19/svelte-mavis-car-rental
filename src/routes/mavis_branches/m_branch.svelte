<script context="module">    
    import { createClient } from '@supabase/supabase-js';  
    

    const SUPABASE_URL = 'https://vhjdmjrluctpaljlzggc.supabase.co';
    const SUPABASE_ANON_KEY = '';    
    const supabase = createClient(SUPABASE_URL, SUPABASE_ANON_KEY);
  </script>
  
  <script lang="ts">    
    import { onMount } from 'svelte';  
    import { messages } from '../loading_messages.js';
    import { typewriter } from '../transition.js';

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
    async function addNewBranch(m_branch: { branch_code: String; manager: String; branch_address: String; suburb: String; state: String; post_code: Number; phone: String; fax: String; branch_name: String; }[]) {
        const newBranch: Branch = {
            branch_code: '', 
            manager: '',
            branch_address: '',
            suburb: '',
            state: '',
            post_code: 0,
            phone: '',
            fax: '',
            branch_name: ''
        };

        try {
            const { data, error } = await supabase
                .from('m_branch')
                .insert([newBranch]);

            if (error) {
                throw new Error(`Error inserting new branch: ${error.message}`);
            }

            // Add the new branch to the m_branch array
            m_branch = [...m_branch, ...(data ?? [])];

            alert('New branch added successfully!');
        } catch (error) {
            console.error(error);
            alert('An error occurred while adding the new branch.');
        }
    }


    async function updateBranch(branch: Branch) {
        try {
            const { error } = await supabase
                .from('m_branch')
                .update({
                    manager: branch.manager,
                    branch_address: branch.branch_address,
                    suburb: branch.suburb,
                    state: branch.state,
                    post_code: branch.post_code,
                    phone: branch.phone,
                    fax: branch.fax,
                    branch_name: branch.branch_name
                })
                .eq('branch_code', branch.branch_code);

            if (error) {
                throw new Error(`Error updating data: ${error.message}`);
            }

            alert('Data updated successfully!');
        } catch (error) {
            console.error(error);
        }
    }
  
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
    let i = -1;

    onMount(() => {
      const interval = setInterval(() => {
      i += 1;
      i %= messages.length;
      }, 2500);

    return () => {
      clearInterval(interval);
    };
    });

  </script>
  
  <h1>Branches</h1>  
  <button on:click={() => addNewBranch(m_branch)}>New Branch</button>
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
          <th>Actions</th>
        </tr>
      </thead>
      <tbody>
        
        {#each m_branch as branch}
          <tr>
            <td>{branch.branch_code}</td>
                    <td><input type="text" bind:value={branch.manager} /></td>
                    <td><input type="text" bind:value={branch.branch_address} /></td>
                    <td><input type="text" bind:value={branch.suburb} /></td>
                    <td><input type="text" bind:value={branch.state} /></td>
                    <td><input type="number" bind:value={branch.post_code} /></td>
                    <td><input type="text" bind:value={branch.phone} /></td>
                    <td><input type="text" bind:value={branch.fax} /></td>
                    <td><input type="text" bind:value={branch.branch_name} /></td>
                    <td><button on:click={() => updateBranch(branch)}>Update</button></td>
          </tr>         
        {/each}
      </tbody>
    </table>
  {:else}
  {#key i}
	<p in:typewriter={{ speed: 10 }}>
		{messages[i] || ''}
	</p>
{/key}
  {/if}
  