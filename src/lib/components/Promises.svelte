<script>
	let page = 1;
	// normal
	fetch(`https://jsonplaceholder.typicode.com/posts?_page=${page}&_limit=10%60`)
		.then((response) => {
			return response.json();
		})
		.then((json) => {
			console.log(json);
		});

	// async await

	let fetchData = async () => {
		let response = await fetch(
			`https://jsonplaceholder.typicode.com/posts?_page=${page}&_limit=10%60`
		);
		let json = await response.json();
		return json;
	};

	fetchData()
		.then((result) => {
			console.log(result);
			return result;
		})
		.catch((err) => {
			console.log(err);
			return err;
		});

	//async await and try catch
	let fetchTryCatch = async () => {
		let response1 = null;
		try {
			response1 = await fetch(
				`https://jsonplaceholder.typicodeERROR.com/posts?_page=1&_limit=10%60`
			);
		} catch (error) {
			//console.log(error);
		}
		let json1 = null;
		try {
			json1 = await response1.json();
		} catch (error) {
			console.log(error);
		}
		let response2 = null;
		try {
			response2 = await fetch(`https://jsonplaceholder.typicode.com/posts?_page=2&_limit=10%60`);
		} catch (error) {
			console.log(error);
		}
		let json2 = await response2.json();

		return { json1: json1, json2: json2 };
	};

	fetchTryCatch()
		.then((result) => {
			console.log(result);
			return result;
		})
		.catch((err) => {
			console.log(err);
			return err;
		});

	let promisesArr = [fetchTryCatch(), fetchTryCatch(), fetchTryCatch(), fetchData()];
	//Promise.all()
	Promise.all(promisesArr)
		.then((result) => {
			console.log(result);
		})
		.catch((err) => {
			console.log(err);
		});
</script>
