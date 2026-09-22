<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>LED Light Up Reading Glasses</title>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/mammoth/1.6.0/mammoth.browser.min.js"></script>
  <style>
    body {
      font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
      max-width: 800px;
      margin: 40px auto;
      padding: 0 20px;
      color: #24292e;
      line-height: 1.6;
    }
    #content img {
      max-width: 100%;
      height: auto;
      display: block;
      margin: 20px 0;
      border-radius: 8px;
      box-shadow: 0 2px 8px rgba(0,0,0,0.1);
    }
  </style>
</head>
<body>
  <div id="content">Loading document...</div>

  <script>
    // Targets your exact document name on GitHub: Instructables (1).docx
    const fileName = encodeURIComponent('Instructables (1).docx');

    fetch(fileName)
      .then(response => {
        if (!response.ok) {
          throw new Error('File not found or failed to load. (HTTP ' + response.status + ')');
        }
        return response.arrayBuffer();
      })
      .then(buffer => mammoth.convertToHtml({ arrayBuffer: buffer }))
      .then(result => {
        document.getElementById('content').innerHTML = result.value;
      })
      .catch(err => {
        document.getElementById('content').innerHTML = `
          <div style="color: #d73a49; border: 1px solid #fdaeb7; padding: 15px; border-radius: 6px; background: #ffeef0;">
            <h3>Unable to load document</h3>
            <p>${err.message}</p>
          </div>`;
        console.error(err);
      });
  </script>
</body>
</html>
