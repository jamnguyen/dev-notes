## Dictionary Object

I saw this many times, in may projects, people try to get item from the array like this:

```ts
const result = [];
users.forEach(user => {
  const isValid = !!validUsers.find(vUser => vUser.id === user.id);
  if (isValid) {
    result.push(user);
  }
});
```

Looping through an array is not a quick operation and even worse if it's long or inside another loop. If you found you need to query your array a lot, consider making it a dictionary object:

```ts
const validUserObj = validUsers.reduce((acc, cur) => ({
  ...acc,
  [cur.id]: cur
}), {});

const result = [];
users.forEach(user => {
  if (!!validUserObj[user.id]) {
    result.push(user);
  }
});
```
