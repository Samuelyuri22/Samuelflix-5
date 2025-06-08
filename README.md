# <!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <title>Catálogo de Filmes</title>
  <style>
    body { font-family: sans-serif; padding: 20px; }
    .container { display: flex; flex-wrap: wrap; gap: 20px; }
    .card {
      width: 300px;
      border: 1px solid #ccc;
      padding: 10px;
      border-radius: 8px;
    }
    iframe, video {
      width: 100%;
      height: 200px;
      border-radius: 4px;
    }
  </style>
</head>
<body>

<h1>Meu Catálogo de Filmes</h1>

<h3>Adicionar Filme:</h3>
<input type="text" id="title" placeholder="Título do filme"><br><br>
<input type="file" id="fileInput" accept="video/*"><br><br>
<input type="text" id="youtubeInput" placeholder="Link do YouTube"><br><br>
<textarea id="desc" placeholder="Descrição" rows="3" cols="40"></textarea><br><br>
<button onclick="addMovie()">Adicionar</button>

<h2>Filmes:</h2>
<div class="container" id="gallery"></div>

<script>
  function addMovie() {
    const title = document.getElementById("title").value;
    const youtubeUrl = document.getElementById("youtubeInput").value;
    const fileInput = document.getElementById("fileInput");
    const desc = document.getElementById("desc").value;

    const card = document.createElement("div");
    card.className = "card";

    const titleEl = document.createElement("h3");
    titleEl.innerText = title;

    const descEl = document.createElement("p");
    descEl.innerText = desc;

    if (youtubeUrl) {
      const videoId = youtubeUrl.split("v=")[1]?.split("&")[0];
      const iframe = document.createElement("iframe");
      iframe.src = `https://www.youtube.com/embed/${videoId}`;
      iframe.allow = "accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture";
      iframe.allowFullscreen = true;
      card.appendChild(iframe);
    } else if (fileInput.files.length > 0) {
      const video = document.createElement("video");
      video.controls = true;
      video.src = URL.createObjectURL(fileInput.files[0]);
      card.appendChild(video);
    }

    card.appendChild(titleEl);
    card.appendChild(descEl);
    document.getElementById("gallery").appendChild(card);

    // Limpar campos
    document.getElementById("title").value = '';
    document.getElementById("youtubeInput").value = '';
    document.getElementById("fileInput").value = '';
    document.getElementById("desc").value = '';
  }
</script>

</body>
</html>
