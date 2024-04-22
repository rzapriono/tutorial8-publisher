# Understanding publisher and message broker.

a. How many data your publisher program will send to the message broker in one run? <br>
Pada program publisher ini terdapat lima pesan yang dikirim ke message broker dalam sekali dijalankan. Hal ini ditandai dengan adanya lima fungsi call `publish_event` yang mengirim pesan berupa `UserCreatedEventMessage`. Isi dari pesan tersebut adalah `user_id` dan `user_name` yang berbeda di tiap fungsi call nya, yakni sebagai berikut.
1. user_id: "1", user_name: "2206827945-Amir"
2. user_id: "2", user_name: "2206827945-Budi"
3. user_id: "3", user_name: "2206827945-Cica"
4. user_id: "4", user_name: "2206827945-Dira"
5. user_id: "5", user_name: "2206827945-Emir"

b. The url of: “amqp://guest:guest@localhost:5672” is the same as in the subscriber program, what does it mean? <br>
URL tersebut berfungsi sebagai alamat dari message broker yang digunakan. Program subscriber dan publisher memiliki URL yang sama karena kedua program dibuat agar saling terhubung dan berkomunikasi melalui message broker yang sama, yakni RabbitMQ. Subscriber dan publisher berinteraksi melalui RabbitMQ sebagai titik sentral. Dengan demikian, saat publisher mengirim pesan ke queue di RabbitMQ, subscriber akan mengatur listener untuk menerima dan memproses pesan dari queue tersebut. Oleh karena itu, subscriber dan publisher harus terhubung ke message broker yang sama agar komunikasi antar keduanya dapat berjalan dengan lancar.

# Running RabbitMQ as message broker.
![Running RabbitMQ](./img/Running-RabbitMQ.png)

# Sending and processing event.
Berikut adalah screenshot terminal dimana subscriber telah berhasil menerima 5 event message broker dari publisher.
![Sending and processing event.](./img/Sending_and_Processing_Event.png)
Setelah menjalankan cargo run di subscriber dan publisher, maka data dari publisher akan dikirim ke message queue yang ada. Kemudian, subscriber akan menerima data dari message queue tersebut dan ditampilkan pada console/terminal.

# Monitoring chart based on publisher.
![Chart](./img/Chart.png)
Berdasarkan screenshot tersebut, terlihat bahwa terdapat spike pada message rates. Peningkatan message rates tersebut disebabkan karena dijalankannya cargo run beberapa kali pada publisher, sehingga terjadi pengiriman message setiap kali cargo run dijalankan. Maka, message rates di RabbitMQ akan meningkat berdasarkan message queue nya.
