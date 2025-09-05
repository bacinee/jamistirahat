<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>OCR Gambar ke Teks - Tesseract.js</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      max-width: 600px;
      margin: 40px auto;
      padding: 20px;
      background: #f9f9f9;
      color: #333;
      box-shadow: 0 0 10px rgba(0,0,0,0.1);
      border-radius: 8px;
    }
    h1 {
      text-align: center;
      color: #2c3e50;
    }
    .input-group {
      margin: 20px 0;
      display: flex;
      justify-content: center;
      gap: 10px;
    }
    select, input[type="file"], button {
      padding: 10px;
      font-size: 16px;
      border-radius: 5px;
      border: 1px solid #ccc;
    }
    button {
      cursor: pointer;
      background-color: #3498db;
      color: white;
      border: none;
      transition: background-color 0.3s ease;
    }
    button:hover {
      background-color: #2980b9;
    }
    #result {
      white-space: pre-wrap;
      min-height: 150px;
      padding: 15px;
      background: #fff;
      border: 1px solid #ddd;
      border-radius: 5px;
      overflow-y: auto;
      font-family: 'Courier New', Courier, monospace;
      font-size: 16px;
    }
    #loading {
      text-align: center;
      color: #888;
      margin-top: 10px;
      font-style: italic;
    }
  </style>
</head>
<body>

  <h1>OCR Gambar ke Teks</h1>

  <div class="input-group">
    <input type="file" id="upload" accept="image/*" />
    <select id="language">
      <option value="eng">English</option>
      <option value="ind">Indonesia</option>
    </select>
  </div>

  <div class="input-group">
    <button id="btnExtract">Ekstrak Teks</button>
    <button id="btnReset" disabled>Reset</button>
  </div>

  <div id="loading"></div>

  <h2>Hasil Teks:</h2>
  <pre id="result"></pre>

  <!-- Load Tesseract.js -->
  <script src="https://cdn.jsdelivr.net/npm/tesseract.js@4/dist/tesseract.min.js"></script>
  <script>
    const upload = document.getElementById('upload');
    const btnExtract = document.getElementById('btnExtract');
    const btnReset = document.getElementById('btnReset');
    const result = document.getElementById('result');
    const loading = document.getElementById('loading');
    const languageSelect = document.getElementById('language');

    let selectedFile = null;

    upload.addEventListener('change', (e) => {
      selectedFile = e.target.files[0];
      result.textContent = '';
      loading.textContent = '';
      btnReset.disabled = !selectedFile;
    });

    btnExtract.addEventListener('click', () => {
      if (!selectedFile) {
        alert('Silakan pilih gambar terlebih dahulu!');
        return;
      }

      loading.textContent = 'Memproses gambar, mohon tunggu...';
      result.textContent = '';
      btnExtract.disabled = true;
      btnReset.disabled = false;

      const reader = new FileReader();
      reader.onload = () => {
        Tesseract.recognize(
          reader.result,
          languageSelect.value,
          {
            logger: m => {
              // Kamu bisa menampilkan progres di sini kalau mau
              // console.log(m);
            }
          }
        ).then(({ data: { text } }) => {
          loading.textContent = '';
          result.textContent = text.trim() || '(Tidak ada teks yang terdeteksi)';
          btnExtract.disabled = false;
        }).catch(err => {
          loading.textContent = '';
          result.textContent = 'Error: ' + err.message;
          btnExtract.disabled = false;
        });
      };
      reader.readAsDataURL(selectedFile);
    });

    btnReset.addEventListener('click', () => {
      upload.value = '';
      selectedFile = null;
      result.textContent = '';
      loading.textContent = '';
      btnReset.disabled = true;
      btnExtract.disabled = false;
    });
  </script>
</body>
</html>
