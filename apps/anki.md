## Anki useful snippets

1.  Border text to **highlight** the concept
<details>
    <summary>
        <strong>Bordered</strong> text with HTML + inline CSS ~ <strong>table</strong>:
    </summary>
    <p>

```xml
<div style="border: 1px solid black; display: inline-block; padding: 15px;">Question word + <b>DO (DOES)</b> + подлежащее + 1 форма:</div>
```

</p>
</details>
<br>

2. Block of code with CSS
<details>
<summary>
    <strong>CodeBlock</strong> with CSS and media query:
</summary>
<p>

```html
<div><br /></div>
<div class="codeblock">
  <pre>
    <!-- put your code here -->
    </pre>
</div>
<div><br /></div>
```

```css
/* put these styles on the very bottom of ANKI HTML */
<style>
   code {
    color: #434343;
    background: #f8f8f8;
  }
    
  .codeblock {
    display: inline-block;
    padding: 15px;
    background-color: #f9f9f9;
    border: 1px solid black;
    text-align: left;
  }

  .codeblock pre {
    margin: 0;
    font-family: inherit;
  }

  @media (max-width: 600px) {
    /* to avoid horizontal scroll on mobiles */
    .codeblock pre {
      white-space: normal;
    }
  }
</style>
```

</p>
</details>
<br>

3. Horizontal rule (HR)
<details>
<summary>
    <strong>Horizontal ruler</strong> to split concepts:
</summary>
<p>

```xml
<br><div><hr></div><br>
```

</p>
</details>
<br>
