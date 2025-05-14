import zipfile
import os

# Direktori dan struktur file
project_name = "promochery"
base_path = f"/mnt/data/{project_name}"
images_path = os.path.join(base_path, "images")
os.makedirs(images_path, exist_ok=True)

# HTML utama
index_html = """<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Promochery - Jual Mobil Chery</title>
  <link href="https://cdn.jsdelivr.net/npm/tailwindcss@2.2.19/dist/tailwind.min.css" rel="stylesheet">
</head>
<body class="bg-gray-100 font-sans">
  <header class="bg-red-600 text-white p-4">
    <div class="container mx-auto flex justify-between items-center">
      <h1 class="text-2xl font-bold">Promochery</h1>
      <div>
        <a href="https://wa.me/6289517530559" class="mr-4 hover:underline">WhatsApp</a>
        <a href="https://instagram.com/rizkisaputra.chry" target="_blank" class="hover:underline">Instagram</a>
      </div>
    </div>
  </header>

  <section class="bg-white py-12 text-center">
    <h2 class="text-3xl font-bold text-gray-800">Promo Mobil Chery Terbaik!</h2>
    <p class="mt-2 text-gray-600">Dapatkan penawaran spesial untuk mobil Chery impian Anda</p>
  </section>

  <section class="py-10">
    <div class="container mx-auto">
      <h3 class="text-xl font-semibold mb-6 text-center">Daftar Mobil</h3>
      <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
        <div class="bg-white rounded-lg shadow p-4">
          <img src="images/tiggo7pro.jpg" alt="Tiggo 7 Pro" class="rounded mb-4">
          <h4 class="text-lg font-bold">Chery Tiggo 7 Pro</h4>
          <p class="text-sm text-gray-600">Harga mulai Rp 380 juta</p>
        </div>
        <div class="bg-white rounded-lg shadow p-4">
          <img src="images/tiggo8pro.jpg" alt="Tiggo 8 Pro" class="rounded mb-4">
          <h4 class="text-lg font-bold">Chery Tiggo 8 Pro</h4>
          <p class="text-sm text-gray-600">Harga mulai Rp 520 juta</p>
        </div>
        <div class="bg-white rounded-lg shadow p-4">
          <img src="images/omoda5.jpg" alt="Omoda 5" class="rounded mb-4">
          <h4 class="text-lg font-bold">Chery Omoda 5</h4>
          <p class="text-sm text-gray-600">Harga mulai Rp 340 juta</p>
        </div>
      </div>
    </div>
  </section>

  <section class="bg-white py-10">
    <div class="container mx-auto max-w-xl">
      <h3 class="text-xl font-semibold mb-4 text-center">Hubungi Kami</h3>
      <form action="https://wa.me/6289517530559" method="get" target="_blank" class="space-y-4">
        <input type="text" placeholder="Nama Anda" required class="w-full p-2 border rounded">
        <input type="tel" placeholder="Nomor HP" required class="w-full p-2 border rounded">
        <textarea placeholder="Pesan atau pertanyaan" rows="4" required class="w-full p-2 border rounded"></textarea>
        <button type="submit" class="w-full bg-red-600 text-white p-2 rounded hover:bg-red-700">Kirim via WhatsApp</button>
      </form>
    </div>
  </section>

  <section class="py-10 bg-gray-100">
    <div class="container mx-auto text-center">
      <h3 class="text-xl font-semibold mb-4">Lokasi Showroom</h3>
      <img src="images/lokasi-showroom.jpg" alt="Lokasi Showroom" class="mx-auto rounded shadow">
    </div>
  </section>

  <footer class="bg-red-600 text-white text-center p-4">
    <p>&copy; 2025 Promochery. Semua Hak Dilindungi.</p>
  </footer>
</body>
</html>"""

# Simpan index.html
with open(os.path.join(base_path, "index.html"), "w") as f:
    f.write(index_html)

# Dummy gambar kosong
dummy_image = b"\x89PNG\r\n\x1a\n" + bytes([0] * 100)

image_files = ["tiggo7pro.jpg", "tiggo8pro.jpg", "omoda5.jpg", "lokasi-showroom.jpg"]
for image_name in image_files:
    with open(os.path.join(images_path, image_name), "wb") as f:
        f.write(dummy_image)

# Buat file ZIP
zip_path = f"/mnt/data/{project_name}.zip"
with zipfile.ZipFile(zip_path, "w") as zipf:
    for root, _, files in os.walk(base_path):
        for file in files:
            file_path = os.path.join(root, file)
            arcname = os.path.relpath(file_path, base_path)
            zipf.write(file_path, arcname=arcname)

zip_path
