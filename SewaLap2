print("FUTSAL 46")
print("Harga jam siang = 50000")
print("Harga jam siang = 80000")


siang = 50000
malam = 80000
BATAS_MALAM = 18

list_hari = ["senin", "selasa", "rabu", "kamis", "jumat", "sabtu", "minggu"]
list_jam = [
    "09:00", "10:00", "11:00", "12:00", "13:00", "14:00",
    "15:00", "16:00", "17:00", "18:00", "19:00", "20:00", "21:00"
]

#storage
pemboking = {}


def book():

  nama = input("masukkan nama pemesan : ")

  print("FUTSAL 46")
  print("Berikut ini hari yang bisa dipesan : ")
  for hari in list_hari:#Menampilkan Hari
    print(hari)
  hari = input("masukkan hari : ").lower()

  #Handling hari
  if hari not in list_hari:
    print("harap masukkan hari yang valid ")
    input("enter kembali .. ")
    return book()

  print("Berikut ini jam yang bisa dipesan")
  for jam in list_jam:
    print(jam)
  jam_mulai = input("masukkan jam : ")

  #Handling jam
  if jam_mulai not in list_jam:
    print("harap masukan jam yang valid ")
    input("enter kembali ..")
    return book()

  #menghilangkan titik dua dan 0, misal 12:00 jadi 12 = bilangan rill
  #sehingga tidak error
  jam_angka_mulai = int(jam_mulai.split(":")[0])

  # handling jam tabrakan / sama
  for pemesan , data in pemboking.items():
     if data["hari"] == hari:
       mulai = int(data["jam"].split(":")[0])
       akhir = data["durasi"]
       if jam_angka_mulai in range(mulai, akhir + mulai):
          print(f"GAGAL , jam {jam_mulai} sudah dibooking oleh {pemesan }")
          print(f" silahkan booking jam lainnya ")
          input("tekan enter untuk kembali")
          return book()
  #Handling
  try:
    durasi = int(input("masukkan durasi 1/2/3/.../12 jam : "))
    if durasi == 0:
      print("Durasi harus lebih dari 0")
      return book()
  except ValueError :
    print("durasi harus angka")
    return book()


  #handling durasi tabrakan terisi / belum
  cek_tersedia = []

  for i in range(durasi):
     cek_tersedia.append(jam_angka_mulai + i)

  for pemesan , data in pemboking.items():
     if data["hari"] == hari:
       mulai = int(data["jam"].split(":")[0])
       akhir = data["durasi"]
       for j in range(durasi):
         jam_terisi = mulai + j
         if jam_terisi in cek_tersedia:
                  print(f"GAGAL! anda menabrak bookingan {pemesan} di jam {jam_terisi}:00")
                  return book()


  total_bayar = 0
  rincian_jam = []

  for i in range(durasi):
    # print(f"\n[Putaran ke-{i+1} , {jam_angka_mulai} , {total_bayar}] (Nilai i = {i})")
    cek_jam = jam_angka_mulai + i

    # print(f"  > Sedang mengecek jam: {cek_jam}:00")

    if cek_jam >= 21:
      print("maaf sudah tutup ")
      return

    if cek_jam >= BATAS_MALAM:
      harga = malam
      status = "malam"

    if cek_jam < BATAS_MALAM:
      harga = siang
      status = "siang"
    # print(f"  > Status: {status} | Harga: Rp {harga}")
    total_bayar += harga
    rincian_jam.append(f"{cek_jam}:00 ({status})")




  print("BOOKING BERHASIL")
  print(f"Nama : {nama} ")
  print(f"total_bayar : {total_bayar}")
  print(f"rincian jam : {rincian_jam}")
  print(f"Hari : {hari}")

  pemboking[nama] ={
      "hari" : hari,
      "jam" :  jam_mulai,
      "durasi" : durasi,
      "total_bayar" : total_bayar,
      "rincian_jam": rincian_jam
  }



##Perintah Cek Ketersediaan
def tersedia():
  for hari in list_hari :
    print(f"{hari}")

  cari_hari = input("Masukkan hari : ").lower()

  if cari_hari not in list_hari :
    print("hari apa yang ko masukkan we , yang benar aja ")

  jam_terisi ={}

  for pemesan , data in pemboking.items():
    if data["hari"] == cari_hari:
      jam_mulai = int(data["jam"].split(":")[0])#menghilangkan titik dua dan 0
      durasi = data["durasi"]
      for i in range(durasi):
        jam_dibook = jam_mulai + i
        jam_terisi[jam_dibook] = pemesan


  print(f"\nStatus Lapangan Hari {cari_hari.lower()}:")
  print("-" * 40)
  print(f"{'JAM':<10} | {'STATUS':<20}")
  print("-" * 40)

  for jamnya in list_jam:
    jam_angka = int(jamnya.split(":")[0])

    if jam_angka in jam_terisi:
      peminjam = jam_terisi[jam_angka]
      print(f"{jamnya:<10} [TERISI  /({peminjam})]")
    else:
      print(f"{jamnya:<10} [KOSONG / TERSEDIA]")

##Perulangan Perintah
while True:
  print("""
  1. Booking Lapangan
  2. cek Ketersediaan
  3. akhiri program
  """)
  pilihan = input("masukkan pilihan :")
  if pilihan == "1":
    book()
  elif pilihan == "2":
    tersedia()
  elif pilihan == "3":
    print("terimakasih sudah menggunakan program ")
    break
  else :
    print("Not Valid")
