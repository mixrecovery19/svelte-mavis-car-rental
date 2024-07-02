<script>
   import '@picocss/pico';
  </script>
  
  <style>
    .container {
      text-align: center;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      min-height: 100vh;
    }    
    .buttons {
      display: flex;
      flex-direction: row;
      gap: 10px;
    }
    button {
      padding: 10px 20px;
      font-size: 16px;
      cursor: pointer;
    }
  </style>
  <slot/>
  <div class="container">
    <h1>Mavis Car Rental</h1>
    <div class="buttons">
      <button on:click={() => window.location.href='./mavis_branches'}>Branches</button>
      <button on:click={() => window.location.href='./mavis_customers'}>Customers</button>
      <button on:click={() => window.location.href='./mavis_fees'}>Fees</button>
      <button on:click={() => window.location.href='./mavis_finished_product_parts'}>Finished Product Parts</button>
      <button on:click={() => window.location.href='./mavis_parts'}>Parts</button>
      <button on:click={() => window.location.href='./mavis_payment'}>Payment</button>
      <button on:click={() => window.location.href='./mavis_plant_parts'}>Plant Parts</button>
      <button on:click={() => window.location.href='./mavis_plants'}>Plants</button>
      <button on:click={() => window.location.href='./mavis_products'}>Products</button>
      <button on:click={() => window.location.href='./mavis_prospects'}>Prospects</button>
      <button on:click={() => window.location.href='./mavis_rental'}>Rental</button>
      <button on:click={() => window.location.href='./mavis_suppliers'}>Suppliers</button>
      <button on:click={() => window.location.href='./mavis_type'}>Type</button>
      <button on:click={() => window.location.href='./mavis_vehicle'}>Vehicle</button>
    </div>
  </div>