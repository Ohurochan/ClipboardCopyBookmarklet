# ClipboardCopyBookmarklet
Javascript Bookmarklet : copy the short url to clipboard

# Usage
1. Get your API Key from Google
  https://developers.google.com/url-shortener/v1/getting_started#APIKey
2. Add this code to your bookmark

  ```javascript
  javascript: var googleApiKey = 'XXXXX'; var global=window; var shortUrl = "initial"; global.COPY_TO_CLIPBOARD=global.COPY_TO_CLIPBOARD||{}; global.COPY_TO_CLIPBOARD.copyToClipboard=function(){ console.log("copy called"); console.log("create short!", shortUrl); var input = document.createElement('input'); input.setAttribute('id', 'copyinput'); document.body.appendChild(input); input.value = shortUrl; input.select(); var ret = document.execCommand('copy'); document.body.removeChild(input); console.log(ret); }; global.COPY_TO_CLIPBOARD.getUrlInfo=function(){ var xhr = new XMLHttpRequest(); var url = 'https://www.googleapis.com/urlshortener/v1/url?key=' + googleApiKey; xhr.open('POST', url, true); xhr.setRequestHeader('Content-type', 'application/json'); xhr.onreadystatechange = function () { if (xhr.readyState === 4) { if (xhr.status === 200) { var json = JSON.parse(xhr.responseText); console.log(json.id); shortUrl = json.id; } else { alert('Shortener error: ' + xhr.responseText); } } }; var data = JSON.stringify({'longUrl': window.location.href}); xhr.send(data); }; global.COPY_TO_CLIPBOARD.getUrlInfo(); var result = ""; window.setTimeout( function() { result = global.COPY_TO_CLIPBOARD.copyToClipboard() }, 1000 ); console.log("result:", result);)
  ```
  
3. Change "XXXXX" to your API Key
  ```javascript
  var googleApiKey = 'XXXXX'; // Change to your API Key
  ```
4. Press bookmark button where you want to get short URL
5. You got short URL in Clipboard !
