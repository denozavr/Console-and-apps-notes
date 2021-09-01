

### Useful console scripts

1. Open all `details/summary` tags in GitHub
```javascript
// `$$` = document.querySelectorAll 
$$('#readme summary').forEach((x) => x.click())
```