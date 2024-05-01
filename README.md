## Reflection

1. What are the key differences between unary, server streaming, and bi-directional streaming RPC (Remote Procedure Call) methods, and in what scenarios would each be most suitable?
   #### Jawab :
   - Unary RPC adalah model panggilan jarak jauh yang paling umum, di mana klien mengirim satu permintaan dan menerima satu respons. Cocok untuk skenario seperti permintaan data yang spesifik atau operasi CRUD sederhana.
   - Server Streaming RPC mengirim satu permintaan dan menerima aliran data dari server. metode ini cocok untuk skenario seperti streaming data secara real-time atau ketika server perlu mengirim banyak respons dalam satu permintaan.
   - Bi-directional Streaming RPC memungkinkan komunikasi dua arah secara bersamaan, di mana klien dan server dapat saling bertukar pesan secara real-time. Skenario seperti chat app, real-time collaboration app, atau data monitoring sering menggunakan model ini.

2. What are the potential security considerations involved in implementing a gRPC service in Rust, particularly regarding authentication, authorization, and data encryption?
   #### Jawab :
    - Otentikasi adalah proses mengonfirmasi identitas pengguna. gRPC mendukung berbagai metode otentikasi, seperti token OAuth atau sertifikat TLS.
    - Otorisasi memastikan pengguna memiliki hak akses yang tepat ke sumber daya tertentu. Di Rust, implementasi dapat menggunakan lapisan otorisasi dengan kontrol akses berbasis peran.
    - Enkripsi data penting untuk memastikan komunikasi aman. gRPC menggunakan HTTP/2, yang mendukung TLS untuk enkripsi end-to-end. Penting untuk mengkonfigurasi sertifikat yang benar dan memastikan transportasi data aman.

3. What are the potential challenges or issues that may arise when handling bidirectional streaming in Rust gRPC, especially in scenarios like chat applications?
   #### Jawab :
    - Sinkronisasi data bisa menjadi tantangan saat klien dan server mengirim pesan secara bersamaan. Implementasi yang tepat dari mutex atau alat sinkronisasi lainnya mungkin diperlukan.
    - Manajemen sumber daya seperti memori dan koneksi harus hati-hati untuk mencegah kebocoran memori atau kehabisan sumber daya.
    - Penanganan kesalahan dalam aliran streaming bisa kompleks. Jika terjadi kegagalan, penting untuk memiliki mekanisme yang jelas untuk menangani dan melanjutkan streaming.

4. What are the advantages and disadvantages of using the tokio_stream::wrappers::ReceiverStream for streaming responses in Rust gRPC services?
   #### Jawab :
    Keuntungan: Penggunaan ini menyediakan cara sederhana untuk mengubah tokio_stream menjadi stream yang kompatibel dengan gRPC, memungkinkan respons streaming dari server ke klien. Ini cocok untuk streaming data yang asinkron.
    
    Kerugian: Penggunaan ini mungkin memiliki overhead tambahan dalam hal pemrosesan dan dapat mengakibatkan keterlambatan kecil dalam streaming data. Juga, masalah dengan sinkronisasi dan penyelarasan dapat muncul jika tidak dikelola dengan benar.

5. In what ways could the Rust gRPC code be structured to facilitate code reuse and modularity, promoting maintainability and extensibility over time?
   #### Jawab :
    Yang pertama adalah pemisahan fungsi berdasarkan penggunaannya dengan memisahkan logika bisnis, komunikasi gRPC, dan lapisan data. Gunakan modul dan komponen untuk membagi logika. Selanjutnya pemanfaatan generics dan traits untuk mendukung pola yang fleksibel dan mudah diperluas. Pemisahan kontrak data dengan menggunakan file protokol buffer (proto) untuk mendefinisikan layanan dan pesan, menjaga skema yang terpisah dari implementasi.

6. In the MyPaymentService implementation, what additional steps might be necessary to handle more complex payment processing logic?
   #### Jawab :
    - Validasi data untuk memastikan semua parameter yang dikirim oleh klien valid dan aman.
    - Penanganan transaksi dengan memastikan konsistensi dalam operasi pembayaran. Gunakan mekanisme rollback atau kompensasi untuk menangani kesalahan.

7. What impact does the adoption of gRPC as a communication protocol have on the overall architecture and design of distributed systems, particularly in terms of interoperability with other technologies and platforms?
   #### Jawab :
    - Interoperabilitas memungkinkan komunikasi antar-layanan dengan bahasa dan platform yang berbeda, berkat protokol yang konsisten.
    - Efisiensi karena HTTP/2 mendukung multiplexing, memungkinkan penggunaan koneksi yang lebih baik.
    - Kompleksitas gRPC membutuhkan pemahaman lebih lanjut tentang protokol dan penyetelan konfigurasi yang tepat.

8. What are the advantages and disadvantages of using HTTP/2, the underlying protocol for gRPC, compared to HTTP/1.1 or HTTP/1.1 with WebSocket for REST APIs?
   #### Jawab :
    Keuntungan: HTTP/2 mendukung multiplexing, mengurangi latensi, dan memberikan dukungan streaming yang lebih baik. Ini mengurangi overhead koneksi dan dapat menghemat sumber daya.
    
    Kerugian: Implementasi HTTP/2 lebih kompleks dibandingkan HTTP/1.1. Selain itu, kompatibilitas dengan beberapa perangkat lunak lama mungkin menjadi masalah.

9. How does the request-response model of REST APIs contrast with the bidirectional streaming capabilities of gRPC in terms of real-time communication and responsiveness?
   #### Jawab :
    REST APIs menggunakan model permintaan-tanggapan tradisional, yang cocok untuk operasi sederhana dan tingkat interaksi rendah. Namun, ini bisa menjadi kurang efisien untuk komunikasi real-time.
    
    gRPC dengan streaming dua arah memberikan kemampuan untuk komunikasi real-time, memungkinkan pertukaran pesan yang lebih cepat dan reaktif antara klien dan server.

10. What are the implications of the schema-based approach of gRPC, using Protocol Buffers, compared to the more flexible, schema-less nature of JSON in REST API payloads?
    #### Jawab :
    Pendekatan berbasis skema gRPC dengan protokol buffer memberikan struktur yang kuat, memungkinkan kontrol lebih baik atas tipe data dan versi. Ini dapat meningkatkan efisiensi dan mengurangi kesalahan interpretasi.
    
    JSON pada REST API lebih fleksibel, memungkinkan perubahan tanpa perubahan skema yang besar. Namun, ini bisa menyebabkan ketidakpastian dalam interpretasi data dan kompatibilitas.
