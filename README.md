<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Generador de firma Stopcar</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Arimo:ital,wght@0,400..700;1,400..700&display=swap" rel="stylesheet">

  <style>
    body {
      font-family: "Arimo", sans-serif;
      padding: 20px;
    }
    input, select {
      margin-bottom: 10px;
      width: 300px;
      font-family: "Arimo", sans-serif;
    }
    button {
      font-family: "Arimo", sans-serif;
      cursor: pointer;
    }
    .firma-preview {
      margin-top: 30px;
      border-top: 1px solid #ccc;
      padding-top: 20px;
    }
    textarea {
      font-family: "Arimo", sans-serif;
    }
  </style>
</head>
<body>

  <h2>Generador de Firma Stopcar.</h2>

  <form id="firmaForm">
    <label>Nombre y Apellido:<br><input type="text" id="nombre" required></label><br>
    <label>Puesto/Sector:<br><input type="text" id="puesto" required></label><br>
    <label>Teléfono:<br><input type="text" id="telefono" required></label><br>
    <label>Email:<br><input type="text" id="email" required>@stopcar.com.ar</label><br>
    <label>Sede:<br></label>
        <select name="sede" id="sede">
            <option value="Av. Hipólito Yrigoyen 631, Morón">Morón</option>
            <option value="Av. Pte. Perón 9626, Ituzaingó">Ituzaingó</option>
            <option value="Magallanes 6435, Mar del Plata">Mar del Plata</option>
            <option value="">Remoto/No corresponde</option>
        </select><br><br>
    <button type="submit">Generar Firma</button>
  </form>

  <div class="firma-preview" id="previewContainer" style="display:none;">
    <h3>Vista previa de la firma:</h3>
    <div id="firmaVisual"></div>

    <div style="margin-top: 15px;">
      <button id="copyButton" onclick="copiarFirma()">Copiar firma</button>
    </div>

    <textarea id="output" rows="10" cols="80" style="margin-top: 20px; display:none;"></textarea>
  </div>

  <script>
    document.getElementById('firmaForm').addEventListener('submit', function(e) {
      e.preventDefault();

      const nombre = document.getElementById('nombre').value.trim();
      const puesto = document.getElementById('puesto').value.trim();
      const telefono = document.getElementById('telefono').value.trim();
      const email = document.getElementById('email').value.trim();
      const sede = document.getElementById('sede').value.trim();

      const firmaHTML = `
<table cellpadding="0" cellspacing="0" border="0" style="font-family: 'Arimo', sans-serif; color: #a31c35;">
  <tr>
    <td style="padding-right: 20px; padding-left: 20px">
      <img src="https://www.stopcar.com.ar/images/FirmaNueva.png" alt="Logo" width="150" style="display: block;">
    </td>
    <td style="padding: 10px 0px;">
      <div style="font-size: 16px; font-weight: bold; color: #a31c35;">${nombre}</div>
      <div style="font-size: 12px; margin-top: 10px; line-height: 16px;font-weight: bold;font-style:italic;">${puesto}</div>
      <div style="font-size: 12px; line-height: 16px;">Tel:
        <a href="tel:+54${telefono}" style="color: #a31c35;text-decoration: none;">${telefono}</a>
      </div>
      <div style="font-size: 12px; line-height: 16px;">
        <a href="mailto:${email}@stopcar.com.ar" style="color: #a31c35; text-decoration: none;">${email}@stopcar.com.ar</a>
      </div>
      <div style="font-size: 12px; line-height: 16px;">
        <a href="https://www.stopcar.com.ar" style="color: #a31c35; text-decoration: none;">www.stopcar.com.ar</a>
      </div>
      <div style="font-size: 12px;line-height: 16px;">${sede}</div>
      <div style="font-size: 12px;line-height: 16px;font-weight: bold;font-style:italic;">Mitesia S.A / Agente Institorio N° 207</div>
    </td>
  </tr>
</table>`;

      document.getElementById('firmaVisual').innerHTML = firmaHTML;
      document.getElementById('output').value = firmaHTML;
      document.getElementById('previewContainer').style.display = 'block';
    });

    // ✅ Copiar la vista previa HTML con formato
    async function copiarFirma() {
      const firmaDiv = document.getElementById('firmaVisual');
      const html = firmaDiv.innerHTML;

      try {
        await navigator.clipboard.write([
          new ClipboardItem({
            "text/html": new Blob([html], { type: "text/html" }),
            "text/plain": new Blob([firmaDiv.innerText], { type: "text/plain" })
          })
        ]);
        alert("✅ Firma copiada.");
      } catch (err) {
        console.error("Error al copiar: ", err);
        alert("❌ No se pudo copiar la firma.");
      }
    }
  </script>

</body>
</html>
