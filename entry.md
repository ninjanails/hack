---
layout: default
---

## Generate `_entries/yourhack.md`

This form will generate the data for you to paste in to Github to create your hack entry.

1. Fill out the form
2. Hit "Generate!"
3. Copy the output text
4. Go to the Render Hack Github repo and [create a file](https://github.com/jsoxford/hack/new/master/_entries?filename=yourhack.md) at `_entries/yourhack.md` (make sure you use an appropriate filename!)
5. Paste your text
6. Submit a new [_Pull Request_](https://github.com/jsoxford/hack/compare?expand=1)

One of our beautiful helpers will check & merge your PR.


<form id="form">
  <div class="field">
    <label for="name">Name of your hack</label>
    <input type="text" name="name" id="name">
  </div>
  <div class="field">
    <label for="url">URL of your hack</label>
    <input type="text" name="url" id="url">
  </div>
  <div class="field">
    <label for="guide">Guide</label>
    <select name="guide" id="guide">
      {% for guide in site.data.guides %}
        <option value="{{ guide.index }}">{{ guide.name }} ({{ guide.technology }})</option>
      {% endfor %}
    </select>
  </div>
  <div class="field">
    <label for="description">Description (can use markdown)</label>
    <textarea name="description" id="description"></textarea>
  </div>
  <button id="submit">Generate!</button>
  <div class="field">
    <label for="output">Output</label>
    <textarea id="output" onclick="this.focus();this.select()" readonly="readonly"></textarea>
  </div>
</form>


<script>
  (function () {
    'use strict';

    document.getElementById('form').addEventListener('submit', function (e) {
      e.preventDefault();
    });

    const fields = ['name', 'url', 'guide', 'description']
    let values = {
      name: '',
      url: '',
      guide: '',
      description: ''
    };

    document.getElementById('submit').addEventListener('click', function (e) {
      fields.forEach(function (field) {
        values[field] = document.getElementById(field).value
      });

      console.log(values);

      document.getElementById('output').innerText =
`---
name: "${values.name}"
url: "${values.url}"
guide: ${values.guide}
---
${values.description}
`
      ;
    });


  }());
</script>