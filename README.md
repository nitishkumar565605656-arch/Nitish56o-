<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Nitish56o - Photo Gallery</title>
  <link rel="icon" type="image/png" href="https://cdn-icons-png.flaticon.com/512/616/616408.png" />
  <script src="https://cdn.tailwindcss.com"></script>
  <style>
    body {
      background: linear-gradient(135deg, #f9c5d1, #fad0c4);
    }
  </style>
</head>
<body class="min-h-screen">
  <header class="bg-white/80 backdrop-blur-md shadow-md p-4 flex justify-between items-center sticky top-0 z-50">
    <h1 class="text-2xl font-bold text-pink-600 drop-shadow-md">💖 Nitish56o</h1>
    <label class="bg-pink-500 hover:bg-pink-600 text-white px-4 py-2 rounded-lg cursor-pointer transition-all">
      Upload Photo
      <input type="file" accept="image/*" id="uploadInput" class="hidden" />
    </label>
  </header>

  <main class="p-4">
    <div id="gallery" class="columns-2 md:columns-3 lg:columns-4 gap-4 space-y-4"></div>
  </main>

  <script>
    const uploadInput = document.getElementById('uploadInput');
    const gallery = document.getElementById('gallery');

    // Load photos from localStorage
    let images = JSON.parse(localStorage.getItem('photos')) || [];
    renderGallery();

    uploadInput.addEventListener('change', (e) => {
      const file = e.target.files[0];
      if (file) {
        const reader = new FileReader();
        reader.onload = function (event) {
          images.push(event.target.result);
          localStorage.setItem('photos', JSON.stringify(images));
          renderGallery();
        };
        reader.readAsDataURL(file);
      }
    });

    function renderGallery() {
      gallery.innerHTML = '';
      images.forEach((src) => {
        const img = document.createElement('img');
        img.src = src;
        img.className =
          'rounded-xl w-full mb-4 shadow-lg hover:scale-105 hover:shadow-2xl transition-all duration-300';
        gallery.appendChild(img);
      });
    }
  </script>
</body>
</html>

