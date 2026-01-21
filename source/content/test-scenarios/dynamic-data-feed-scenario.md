**UI Approach :**
this approach use more visual interaction and have more complex way.
- **Navigate to a page containing contentful data fetcher**
  Several page have `contentful` data fetcher component such as [[Dynamic Partner Feed Section]], [[Dynamic Insights Feed Section]], [[Dynamic Carousel Feed Section]]. To do this in playwright you can implement code like this :
  ```ts
	await page.goto('https://incentro.com/en-NL/xxx');  
  ```
- **Click each content category button**
  for example, inside Insight [[page]], it's have `Blogs`, `News`, `Events`, `Whitepapers`. we can click each button to refresh the content list. To do this in playwright you can implement code like this :
  ```ts
	await page.getByTestId('submit-btn').click();
  ```
- **Verify the request success and validate data structure**
  after hit, make sure the request get `200`, and make sure it's contain content. To do this in playwright you can implement code like this :
  ```ts
	// replace xxx with incentro category url
	const response = await page.waitForResponse(resp => resp.url().includes('/xxx'))
	expect(response.status()).toBe(200);
  ```

**Functional Approach :**
This approach use less visual interaction and have more straight forward implementation.
- **Provide list of URL that represent contentful data fetcher for each category**
  base on previous approach, each button category represent different URL. to reduce visual dependency, we can create list of URL target and directly hit it. To do this in playwright you can implement code like this :
  ```ts
	const categoryURLs = [
		'https://www.incentro.com/en-NL/insights?contentType=Blog',
		'https://www.incentro.com/en-NL/insights?contentType=Event',
		'https://www.incentro.com/en-NL/insights?contentType=News',
		'https://www.incentro.com/en-NL/insights?contentType=Whitepaper',
		'https://www.incentro.com/en-NL/insights?contentType=Lab'
	]
  ```
- **Hit each provided URL & verify the request success and validate data structure**
  hit every URL inside list that already prepared before. To do this in playwright you can implement code like this :
  ```ts
		const response = await page.waitForResponse(resp => resp.url().includes(categoryURL))
		expect(response.status()).toBe(200);
		// you can validate data structure here inside response variable
  ```