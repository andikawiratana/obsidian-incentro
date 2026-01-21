**Navigate to a page containing a form**
every page level have their own [[Hubspot Form]], and only [[Event Detail Page]] that have [[Eventbrite Form]]. To do this in playwright you can implement code like this :
```ts
await page.goto('https://incentro.com/en-NL/xxx');
```

**Fill form with valid data**
Incentro.com have several [[Hubspot Form]], the most minimal one is for email submission in the footer section. To do this in playwright you can implement code like this :
```ts
// replace xxx with username component selector
// replace yyy with password component selector
await page.getByLabel('xxx').fill(validCredentials.username);
await page.getByLabel('yyy').fill(validCredentials.password);
```

**Intercept API request, to ensure the payload is correct** (*OPTIONAL*)
Cause we use third party to process the submitted data, we can implement request interception to make sure data that we have send is valid. this is optional step cause we can make sure this process valid in previous one. To do this in playwright you can implement code like this :
```ts
// replace xxx with hubspot submission url
await page.route('xxx', async route => {  
	const response = await route.fetch();  
	let body = await response.text(); // <- validate data inside it
	await route.fulfill({  
		response,  
		body,  
		headers: {  
			...response.headers(),  
			'content-type': 'text/html'  
		}  
	});  
});
```

**Verify the success state**
This is final step, when we make sure the request have `200` status code. To do this in playwright you can implement code like this :
```ts
// replace xxx with hubspot submission url
const response = await page.waitForResponse(resp => resp.url().includes('/xxx'))
expect(response.status()).toBe(200);
```
