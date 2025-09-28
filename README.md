<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Upload Audio</title>
  <style>
    ul{
      list-style: none;

    }
    li{
      padding: 10px;
      margin-top: 5px;
    }
    li.response{
      background-color: aqua;
      color: black;
      font-weight: bold;

    }
    li.input{
      background-color: lightgray;
      color: black;
      font-weight: bold;
      text-align: right;
    } 
  </style>
  <script src="https://js.puter.com/v2/"></script>

</head>
<body>
  <script>
    let puterRes = puter.ai.chat("Explain AI like I'm five!").then(puter.print);
    document.write(puterRes);
  </script>
  <h2>Upload Audio to FastAPI</h2>
  
  <!-- Select an audio file -->
  <input type="file" id="audioInput" accept="audio/*">
  <button id="uploadBtn">Upload</button>
  <div></div>
  <ul id="chat"></ul>

  <script>
    async function uploadAudio(file) {
      const formData = new FormData();
      formData.append("file", file);

      const response = await fetch("http://localhost:8000/upload-audio/](https://mc9l4nsk-8000.brs.devtunnels.ms/)", {
        method: "POST",
        body: formData
      })
      .then(res => res.json())
      .then(data => {
        let liInput = document.createElement("li");
        liInput.classList.add("input");
        liInput.textContent = data.input;
        document.getElementById("chat").appendChild(liInput);
        let li = document.createElement("li");
        li.classList.add("response");
        li.textContent = `${data.response}`;
        document.getElementById("chat").appendChild(li);
      })
    }

    document.getElementById("uploadBtn").addEventListener("click", () => {
      const file = document.getElementById("audioInput").files[0];
      if (file) {
        uploadAudio(file);
      } else {
        alert("Please select an audio file first.");
      }
    });
  </script>
</body>
</html>
