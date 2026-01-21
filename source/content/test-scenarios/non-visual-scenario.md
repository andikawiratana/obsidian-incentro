**Provide pair URL that is URL and it's redirection**
To prepare the testing process, we should create pair URL that the old URL and it's redirection. To do this in playwright you can implement code like this :
```ts
const redirections = [{new:'xxx', old:'yyy'}];
```

**Navigate to a page the specific redirection**
Use the previous redirection data to go specific URL. To do this in playwright you can implement code like this :
```ts
// use the previous redirection data
await page.goto(redirection.old)
```

**Validate is redirection successful**
Validate the previous URL hit, is that successfully redirected. To do this in playwright you can implement code like this :
```ts
await expect(page).toHaveURL(redirection.new);
```