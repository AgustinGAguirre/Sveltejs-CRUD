<script>
import { v4 } from "uuid";

	let products = [
		{
			id: 1,
			name: "Apple Macbook Pro",
			description: "Chip M1",
			category: "laptops"
		},
		{
			id: 2,
			name: "Apple AirPods",
			description: "Noise Cancelling",
			category: "peripherals"
		},
	];

	let product = {
		id: "",
		name: "",
		description: "",
		category: "",
		imageURL: "",
	};

	let editStatus = false;

	const addProduct = () => {

		const newProduct = {
			id: v4(),
			name: product.name,
			description: product.description,
			category: product.category,
			imageURL: product.imageURL
		}

		products = products.concat(product)
		cleanProduct();

		console.log(products);
	}

	const updateProduct = () => {
		let updatedProduct = {
			name: product.name,
			description: product.description,
			id: product.id,
			imageURL: product.imageURL,
			category: product.category
		}

		const productIndex = products.findIndex(p => p.id === product.id)
		products[productIndex] = updateProduct;
		cleanProduct();

		editStatus = false;
	}

	const onSubmitHandler = (e) => {
		if (!editStatus){
			addProduct();
		} else {
			updateProduct()
		}
		
	};

	const cleanProduct = () => {
		product = {
		id: '',
		name: '',
		description: '',
		category: '',
		imageURL: ''
		}
	}

	const deleteProduct = (id) => {
		products = products.filter(product => product.id !== id);
	}

	const editProduct = productEdited => {
		product = productEdited;
		editStatus = true;
	}

</script>

<main>
	<div class="container p-4">
		<div class="row">
			<div class="col-md-6">
		
			{#each products as product}
				<div class="card mt-2">
					<div class="row">
						<div class="col-md-4">
							{#if !product.imageURL}
								<img src="images/product-not-found.png" alt="" class="img-fluid p-2">
							{:else}
								<img src="{product.imageURL}" alt="">
							{/if}
						</div>
						<div class="col-md-8">
							<div class="card-body">
								<h5>
									<strong>{product.name}</strong>
									<span>
										<small>
											{product.category}
										</small>
									</span>
								</h5>
								<p class="card-text">{product.description}</p>
								<button class="btn btn-danger" on:click={deleteProduct(product.id)}>
									Delete
								</button>
								<button class="btn btn-secondary" on:click={editProduct(product)}>
									Edit
								</button>
							</div>
						</div>
					</div>
				</div>
			{/each}

			</div>
			<div class="col-md-6">
				<div class="card">
					<div class="card-body">
						<form on:submit|preventDefault={onSubmitHandler}>
							<div class="form-group">
								<input
								bind:value={product.name}
								type="text"
								placeholder="Product Name"
								class="form-control"
							/>
							</div>
							<div class="form-group">
								<textarea
								bind:value={product.description}
								name="product-description"
								rows="3"
								placeholder="Product Description"
								class="form-control"
							/>
							</div>
							<div class="form-group">
								<input
								bind:value={product.imageURL}
								type="url"
								id="product-image-url"
								placeholder="https://google.com/"
								class="form-control"
							/>
							</div>
							<div class="form-group">
								<select
								id="category"
								bind:value={product.category}
								class="form-control"
							>
								<option value="laptops">Laptops</option>
								<option value="peripherials"
									>Peripherials</option
								>
								<option value="phones">Phones</option>
							</select>
							</div>

							<button class="btn btn-secondary">
								{#if !editStatus}
									Save Product
								{:else}
									Update Product
								{/if}
							</button>
						</form>
					</div>
				</div>
			</div>
		</div>
</main>

<style>
</style>
