# Praktikum-Jarkom-Modul-1

# Anggota

| Nama                            | NRP          |
| ------------------------------- | ------------ |
| Marcelinus Alvinanda Chrisantya | `5027221012` |
| Bintang Ryan Wardana            | `5027221022` |

## 1. ATM or ATP or FTP
![Screenshot 2024-03-31 000018](https://github.com/J0see1/Jarkom-Modul-1-IT29-2024/assets/143849730/8579ab34-b0da-4fd6-b026-580ee5ba2d66)

1. Langkah pertama yang dilakukan adalah mencari packet `protocol FTP` yang mengindikasikan adanya request/response terkait dengan login yaitu input username dan password. Ditemukan salah satunya yaitu `response : 331 Please specify the password`
![Screenshot 2024-03-31 000126](https://github.com/J0see1/Jarkom-Modul-1-IT29-2024/assets/143849730/be2cc7eb-9432-4727-8234-df10176f1c64)

2. Kemudian, saya mem-follow packet tersebut untuk melihat semua stream yang serupa
![Screenshot 2024-03-31 000229](https://github.com/J0see1/Jarkom-Modul-1-IT29-2024/assets/143849730/024bd660-d811-41f7-b67a-11d412813b42)
   Untuk mencari password yang correct, saya mengecek satu per satu setiap stream hingga akhirnya menemukan `Login successful` pada stream 319 dengan passwordnya adalah `m4y_th3_Kn!fe_ch1p_&_sh4tter`


## 2. evidence

1. Untuk mencari domain dari client "nanomate", saya menggunakan filter frame dengan nama dari client yaitu nanomate. `frame contains "nanomate"`

![Screenshot 2024-04-03 080333](https://github.com/J0see1/FP-Strukdat/assets/134209563/c8db7c3e-0a90-45d0-951c-30478fd9a75c)

2. Untuk mencari web service yang digunakan dari nanomate, saya melakukan filter "server" pada display filter. `http contains "server"`

![Screenshot 2024-04-03 080626](https://github.com/J0see1/FP-Strukdat/assets/134209563/822b1288-234c-49ce-ae1b-a114f5dbf4ff)

3. Untuk mencari endpoint login website, saya menggunakan filter `http contains "POST"`. Alasannya karena proses login biasanya menggunakan method POST.

![Screenshot 2024-04-03 081146](https://github.com/J0see1/FP-Strukdat/assets/134209563/59443db6-8115-4409-a294-8ae7d5422614)

4. Terakhir untuk melihat email dan password yang berhasil digunakan attacker untuk masuk ke dalam sistem nanomate, saya melakukan filtering kata Login Successful. Berikut querynya `Frame contains "Login Successful"`

![Screenshot 2024-04-03 081628](https://github.com/J0see1/FP-Strukdat/assets/134209563/9d01de9b-0b92-48d0-8d4f-9c8745575727)

5. Berikut tampilan netcat dan flag yang didapat:

![Screenshot 2024-03-31 000531](https://github.com/J0see1/FP-Strukdat/assets/134209563/bcbe9993-22bc-474a-83a6-c362160bafea)


## 3. How Many Packets?
![Screenshot 2024-03-31 000954](https://github.com/J0see1/Jarkom-Modul-1-IT29-2024/assets/143849730/2feb2ef2-fb11-4aed-81cc-de65983e8c90)

1. Dalam melakukan bruteforce login tentunya attacker akan melakukan banyak `login incorrect` dan `1x login succesful`, maka dari itu untuk menghitung total login attempt adalah dengan menjumlahkan total packet dengan response login incorrect dan 1 response login successful. Langkah pertama yang saya lakukan adalah mencari packet dengan info `Login incorrect` secara manual.
![Screenshot 2024-04-01 063254](https://github.com/J0see1/Jarkom-Modul-1-IT29-2024/assets/143849730/bd3ef1ed-9843-457c-92c9-b040234a094e)


3. kemudian melakukan filter `ftp.response.code == 530` untuk menampilkan semua packet dengan info `Login incorrect`
![image](https://github.com/J0see1/Jarkom-Modul-1-IT29-2024/assets/143849730/7bdf278c-5a97-470f-8bb8-5b7db88d9110)

4. Kemudian `apply as filter > selected` untuk melihat total displayed login attempt incorrect yaitu sebanyak `933 login attempt`
![Screenshot 2024-03-31 000718](https://github.com/J0see1/Jarkom-Modul-1-IT29-2024/assets/143849730/0c837a7f-01b8-40a9-8683-967866a7f47a)
![Screenshot 2024-03-31 000742](https://github.com/J0see1/Jarkom-Modul-1-IT29-2024/assets/143849730/cb2f8106-fa2d-496d-8c8b-68dde940c961)

5. Dengan informasi tersebut, dapat dihitung total login attempt yang dilakukan attacker yaitu : 
`Total login attempt : 934` yang terdiri dari
incorrect login attempt : 933
dan correct login attempt : 1


## 4. trace him
![Screenshot 2024-03-31 001249](https://github.com/J0see1/Jarkom-Modul-1-IT29-2024/assets/143849730/bbb1900e-23fb-470f-b94b-b546be3b979a)

1. Untuk mendapatkan IP address attacker maka dapat dilihat melalui salah satu packet, disini packet yang saya analisis adalah packet `Login incorrect` yang merupakan response dari IP server untuk IP attacker. Maka dapat disimpulkan bahwa IP attacker adalah `IP destination` packet tersebut yaitu : `10.30.3.4`
![Screenshot 2024-03-31 001317](https://github.com/J0see1/Jarkom-Modul-1-IT29-2024/assets/143849730/75fde370-a71c-447d-ac08-c0a5044872a4)


## 5. creds

## 6. malwleowleo 

## 7. whoami

## 8. secret

## 9. fuzz

`SOAL - 1`

![Screenshot 2024-03-31 001440](https://github.com/J0see1/Jarkom-Modul-1-IT29-2024/assets/143849730/34657dd2-6d45-4898-b1d7-66513c657670)
1. Untuk menemukan IP address milik attacker, saya mencoba menganalisis salah satu packet yang merupakan packet upaya login oleh attacker. Saya melakukan `filter http` dan mencari packet HTTP POST karena POST berarti attacker mencoba melakukan request berupa login attempt. 
![Screenshot 2024-04-01 072858](https://github.com/J0see1/Jarkom-Modul-1-IT29-2024/assets/143849730/77998657-d71a-4478-9343-449b99a16d0b)
Dapat dilihat pada packet 105 tersebut attacker mencoba melakukan login dengan uname = admin dan password = password, hal ini menjadi bukti bahwa packet ini direquest oleh attacker.  Maka dari itu, `IP source : 10.33.1.154`  tentunya merupakan IP dari requester yaitu attacker itu sendiri.
![Screenshot 2024-04-01 073244](https://github.com/J0see1/Jarkom-Modul-1-IT29-2024/assets/143849730/46800222-e52b-49d2-9977-a416e211d99d)


`SOAL - 2`

![Screenshot 2024-03-31 001749](https://github.com/J0see1/Jarkom-Modul-1-IT29-2024/assets/143849730/07ae4872-1869-4685-acdd-653c1a5379c7)

2. Dengan packet yang dianalisis sebelumnya, ditemukan juga informasi port yang digunakan oleh web server korban yaitu destination port. `Destination port(80)` merupakan port web server korban karena packet tersebut direquest oleh attacker dengan destinasinya adalah web server korban![Screenshot 2024-04-01 073502](https://github.com/J0see1/Jarkom-Modul-1-IT29-2024/assets/143849730/fc0b111a-37a3-4719-bc96-d0acf0ac7f21)

`SOAL - 3 `

![Screenshot 2024-04-03 131550](https://github.com/J0see1/Jarkom-Modul-1-IT29-2024/assets/143849730/fcf8b09c-35ed-464f-80fd-1205abf6dc60)

3. Untuk mengetahui endpoint yang digunakan untuk login, dapat dilihat melalui info packet POST yaitu seperti berikut :
Pada packet tersebut dapat dilihat bahwa endpoint yang digunakan untuk login adalah `/(slash)`.
![Screenshot 2024-04-03 132131](https://github.com/J0see1/Jarkom-Modul-1-IT29-2024/assets/143849730/7c87acb3-bc2b-4040-a1cf-af89064f2da5)

`SOAL - 4`

![Screenshot 2024-03-31 001918](https://github.com/J0see1/Jarkom-Modul-1-IT29-2024/assets/143849730/4b5fcdda-4b57-49a8-a629-fc061c719d9f)

4. Untuk mencari tools yang digunakan oleh attacker, saya menganalisis packet yang sama juga dengan soal sebelumnya yaitu packet 105. Kemudian saya melakukan `follow http stream` packet tersebut dan ditemukan informasi berikut.
Dapat dilihat dengan jelas informasi attacker salah satunya adalah tools yang digunakan yaitu `Fuz Faster U Fool v2.0.0-dev`. Kemudian dengan menyeseuaikan format pertanyaan, tools yang digunakan adalah `ffuf-v2.0.0-dev`

![Screenshot 2024-03-31 001946](https://github.com/J0see1/Jarkom-Modul-1-IT29-2024/assets/143849730/52235edb-0f56-4ef6-a022-d9d0f269d814)

`SOAL - 5`

![Screenshot 2024-03-31 002013](https://github.com/J0see1/Jarkom-Modul-1-IT29-2024/assets/143849730/b209a77e-70c8-4fc8-bdb2-563210b50ef3)

5. Dalam konteks web server, respons `302 found` biasanya digunakan untuk mengarahkan client(dalam hal ini attacker) ke suatu halaman atau url lain setelah client berhasil melakukan login ke web server. Maka dari itu, langkah pertama yang saya lakukan dalah melakukan filter `http.response.code == 302` untuk menemukan packet dengan response 302 found.
   
![Screenshot 2024-03-31 002036](https://github.com/J0see1/Jarkom-Modul-1-IT29-2024/assets/143849730/f66d2570-1709-41c5-816e-4c1d6f930604)
   
Kemudian saya melakukan `follow HTTP stream` terhadap packet tersebut.
![Screenshot 2024-03-31 002103](https://github.com/J0see1/Jarkom-Modul-1-IT29-2024/assets/143849730/e0cc5205-21de-4eff-8399-9601b4aedc8b)

Untuk menemukan login attempt yang berhasil dilakukan attacker, saya melakukan `find : 302 found` pada HTTP Stream tersebut![Screenshot 2024-04-01 075615](https://github.com/J0see1/Jarkom-Modul-1-IT29-2024/assets/143849730/58d34de3-6045-46d8-a891-fca004fdab56)

Setelah melakukan find terhadap HTTP stream tersebut, ditemukan salah satu login attempt dengan code 302 found dan ditemukan juga username beserta password yang berhasil digunakan oleh attacker yaitu `admin:sUp3rSecretp@ssw0rd`![Screenshot 2024-04-01 073709](https://github.com/J0see1/Jarkom-Modul-1-IT29-2024/assets/143849730/bf683b85-e436-4082-93e7-0524bc0e267d)





## 10. malwaew 
