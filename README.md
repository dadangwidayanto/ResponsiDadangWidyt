# ResponsiDadangWidyt
# Membangun apache Spark

Langkah 1 : Masuk atau remote VM menggunakan putty dengan cara memasukkan ip public dari vm kedalam kolom  Host Name (or IP Address) lalu masukkan username dan password VM.


Langkah 2 : ketikkan perintah:

            sudo apt get update 

perintah ini digunakan untuk melakukan update basis data atau paket software lokal dan mengakses versi terbaru


langkah 3 : melakukan instalasi paket java dengan menggunakan perintah :
    
            Sudo apt-get install default-jdk

kemudian cek versi java dengan menggunakan perintah :

            java -version
            

Langkah 4 : Membuat direktori baru menggunakan perintah :

            mkdir /opt/dadang
            
dengan nama dadang didalam direktori opt , direktori baru ini nantinya digunakan utuk menyimpan file extrack dari spark-2.4.7-bin-hadoop2.7.tgz

Langkah 5 : Download apche spark package Selanjutnya kita harus mendownload paket-paket dari apache spark dengan menggunakan perintah dibawah. Untuk mendownload bisa mengakses https://spark.apache.org/downloads.html dan pilih spark yang ingin digunakan dan download. Atau bisa menggunakan perintah dibawah ini :
wget https://downloads.apache.org/spark/spark-2.4.7/spark-2.4.7-bin-hadoop2.7.tgz

Langkah 6 : masuk direktori Untuk menjelajahi file dan direktori Linux, gunakan perintah cd. Perintah Linux ini memerlukan path penuh atau nama direktori, tergantung pada direktori yang digunakan saat ini. Disini Menggunakan perintah:cd /opt/dadang untuk masuk ke direktori dadang.

Langkah 7 : Mengekstak file spark-2.4.7-bin-hadoop2.7.tgz dengan perintah:

            tar -xvf spark-2.4.7-bin-hadoop2.7.tgz
            
Langkah 8 : Configure the Environment Sebelum memulai server master Spark, ada beberapa variabel yang perlu dikonfigurasi.

            vi~/.bashrc

Dan masukkan

            export SPARK_HOME=/opt/reesponsi/spark-2.4.7-bin-hadoop2.7 
            export PATH=$PATH:$SPARK_HOME/bin:$SPARK_HOME/sbin 

Langkah 9 : Menjalankan file master  dengan perintah 

            start-master.sh

Langkah 10 : Test port, Untuk mengetahui port yang listening ke port 8080 maka digunakan perintah 
        
             ss –tunelp |grep 8080
             

Langkah 11 :Membuat file txt dan memberi isi dengan perintah pico

            pico input.text

Text yang dimasukan terserah, atau bisa melihat file input yang ada pada repository ini untuk melihat text yang saya gunakan. Setelah itu di save.

Langkah 12 : Menjalankan apache spark, dengan menggunakan perintah:

            spark-shell

Langkah 13 : Menginputkan perintah val pada scala
Scala adalah bahasa pemrograman yang menggabungkan paradigma pemograman berorientasi objek dengan fungsional. Scala memiliki type system yang kuat dan statis (strong, static type-system). Scala berjalan di atas JVM, dan memiliki interoperability yang kuat dengan Java. Developer bisa dengan mudah meng-import library Java di program berbasis Scala. Scala dirancang sebagai bahasa yang memungkinkan developer membuat kode yang ringkas, fleksibel, namun tetap aman.

Seperti ini tampilan dari spark kita bisa memasukan text didalamnya. Karena tadi sudah dibuatkan sebelumnya jadi kita tinggal memanggil file ke dalam sini dengan cara mengetikan perintah dibawah :

              val inputfile = sc.textFile(“input.text”)

              val counts = inputfile.flatMap(line => line.split(" ")).map(word =>(word, 1)).reduceByKey(+);

              counts.cache()

              counts.saveAsTextFile("output")

Pada perintah saveAsTextFile (“output”) memiliki arti menyimpan file pada directori output.

Langkah 14 : Masuk ke directori output

            cd output/

Setelah itu jalankan perintah dibawah ini untuk melihat hasil atau Melihat isi dari part-00000

            Cat part-00000

