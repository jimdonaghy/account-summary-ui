<script>

	
	const formatter = new Intl.NumberFormat('en-US', {
		style: 'currency',
		currency: 'USD',
		minimumFractionDigits: 2
	})


	let promise = fetch('http://localhost:8083/homedata').then((x) => x.json());
</script>

{#await promise}
	<!-- optionally show something while promise is pending -->
{:then data}
	<!-- promise was fulfilled -->

	<div class="container">
		<h1>Bank Account Summary</h1>
		<p>Account Holder: {data.customer.name} | {data.customer.address} | {data.customer.phone}</p>
		<p>Account Number: {data.account.accountNumber}</p>
		<p>Current Balance ${data.account.balance}.00</p>
	
		<table>
		  <tr>
			<th>Date</th>
			<th>Description</th>
			<th>Amount</th>
		</tr>
		  {#each data.account.transactions as transaction}
		  <tr>
			<td>{transaction.transactionDate}</td>
			<td>{transaction.description}</td>
			<td>${transaction.amount}.00</td>
		  </tr>
		  {/each}
		</table>
	  </div>

{:catch error}
	<!-- optionally show something while promise was rejected -->
{/await}

<style>
    body {
      font-family: Arial, sans-serif;
    }
    .container {
      max-width: 800px;
      margin: 0 auto;
    }
    table {
      width: 100%;
      margin-top: 20px;
    }
    th, td {
      text-align: left;
      padding: 8px;
    }
    th {
      background-color: #4CAF50;
      color: white;
    }
    tr:nth-child(even) {
      background-color: #f2f2f2;
    }
  </style>


