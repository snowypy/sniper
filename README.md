<h3 align="center">

  
  By snowyjs (base by k1zz)
</h3>

## Claim Range
Use the following Javascript bookmarklet in your browser to obtain the droptime while on `namemc.com/search?q=<username>`:

```js
javascript:(function(){function parseIsoDatetime(dtstr) {
    return new Date(dtstr);
};

startElement = document.getElementById('availability-time');
endElement = document.getElementById('availability-time2');

start = parseIsoDatetime(startElement.getAttribute('datetime'));
end = parseIsoDatetime(endElement.getAttribute('datetime'));

para = document.createElement("p");
para.innerText = Math.floor(start.getTime() / 1000) + '-' + Math.ceil(end.getTime() / 1000);

endElement.parentElement.appendChild(para);})();

```

If 3name.xyz has a lower length claim range for a username I would recommend using that, you can get the unix droptime range with this bookmarklet on `3name.xyz/name/<name>`

```js
javascript: (function() {
    startElement = document.getElementById('lower-bound-update');
    endElement = document.getElementById('upper-bound-update');
  
  	if (startElement === null) {
    	startElement = 0;
    } else {
      startElement = startElement.getAttribute('data-lower-bound')
    }
  
  
    para = document.createElement("p");
    para.innerText = Math.floor(Number(startElement) / 1000) + '-' + Math.ceil(Number(endElement.getAttribute('data-upper-bound')) / 1000);
    endElement.parentElement.appendChild(para)
})()
```

## accounts formatting

- place in `gc.txt` or `ms.txt` depending on their account type.
  - `gc.txt` is for accounts without usernames
  - `ms.txt` is for accounts that already have usernames on them
- a bearer token can be obtained by following  [this guide](https://kqzz.github.io/mc-bearer-token/)

```txt
EMAIL:PASSWORD
BEARER
```

### Example accounts files

```txt
kqzz@gmail.com:SecurePassword3
teun@example.com:SafePassword!
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c
```
> This will load 3 accounts into the sniper, two of which are supplied with email / password. The last is loaded by bearer token, and will last 24 hours (the sniper will show the remaining time).

> Their account types are determined by if they are placed in `gc.txt` or `ms.txt`.

## understanding logs

Each request made to change your username will return a 3 digit HTTP status code, the meanings are as follows:

- 400 / 403: Failed to claim username (will continue trying)
- 401: Unauthorized (restart claimer if it appears)
- 429: Too many requests (add more proxies if this occurs frequently)
