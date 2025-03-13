# Tutorial Modul 5
---
> 1. What is the difference between the approach of performance testing with JMeter and profiling with IntelliJ Profiler in the context of optimizing application performance?

Perbedaan utama dari test performance dengan menggunakan JMeter dan IntelliJ Profiler adalah JMeter merupakan sebuah aplikasi yang digunakan untuk menguji beban aplikasi dan mengukur performa aplikasi di berbagai tingkat penggunaan sementara IntelliJ merupakan alat analisis kinerja kode yang membantu pengguna dalam mengidentifikasi penggunaan CPU, memori, dan aktivitas thread.

> 2. How does the profiling process help you in identifying and understanding the weak points in your application?

Profiling dapat membantu saya dalam menemukan metode yang berjalan lambat dan menjadi beban bagi program. Profiler dapat mengukur waktu eksekusi setiap method/fungsi dalam sebuah aplikasi dan dapat menunjukkan metode mana yang berjalan paling lambat sehingga dapat dioptimisasi. Lalu profiler juga membantu saya dalam mendeteksi penggunaan memori karena profiler dapat melacak alokasi dan penggunaan memori dalam aplikasi sehingga mencegah aplikasi mengalami kebocoran memori.

> 3. Do you think IntelliJ Profiler is effective in assisting you to analyze and identify bottlenecks in your application code?

Ya, IntelliJ Profiler sangat efektif dalam membantu saya mengidentifikasi bottleneck karena profiler ini dapat menemukam metode yang membutuhkan eksekusi paling lama, mendeteksi kebocoran memori, menganalisis performa thread, dan juga mengoptimalkan CPU agar aplikasi berjalan lebih responsif

> 4. What are the main challenges you face when conducting performance testing and profiling, and how do you overcome these challenges?

Karena baru kali ini saya melakukan performance testing dan profiling terutama di IntellliJ, saya belum terbiasa terhadap informasi-informasi yang diberikan pada profiler. Banyaknya informasi teknis seperti stack trace, alokasi memori, grafik CPU/Memori dan lain-lain membuat saya menjadi bingung terhadap sebenarnya hal apa yang menjadi beban bagi program. Cara saya dalam mengatasinya adalah dengan lebih sering berinteraksi dengan profiler di IntelliJ dan juga memanfaatkan fitur flame code yang dirancang agar user mudah menemukan flaw di dalam kode.

> 5. What are the main benefits you gain from using IntelliJ Profiler for profiling your application code?

Dengan menggunakan IntelliJ Profiler, saya dapat menemukan bottleneck dan inefisiensi dalam kdoe saya secara cepat berdasarkan waktu method/fungsi saya bekerja. Selain itu saya juga dapat memantau alokasi memori secara real-time, dan memantau thread. Profiling di IntelliJ juga intuitif dan mudah digunakan karena terintegrasi dengan IntelliJ IDEA.

> 6. How do you handle situations where the results from profiling with IntelliJ Profiler are not entirely consistent with findings from performance testing using JMeter?

Jika saya menemukan perbedaan, pertama-tama saya akan mengecek bahwa pengujian di IntelliJ Profiler dilakukan dengan kondisi yang sama seperti apa yang ada di JMeter, contohnya jumlah thread memastikan penggunaan aplikasi dalam beban yang sama. Jumlah thread atau jumlah pengguna yang berbeda di tiap profiler dapat menyebabkan perbedaan hasil testing. Selain itu route ke URL localhost juga harus dicek kembali di JMeter sehingga sama dan akurat terhadap apa yang ingin dites.

> 7. What strategies do you implement in optimizing application code after analyzing results from performance testing and profiling? How do you ensure the changes you make do not affect the application's functionality?

Karena method paling banyak memakan waktu running program adalah method getAllStudentWithCourses() di `StudentService.java`, saya mengimplementasikan optimisasi di method tersebut dengan mengganti keseluruhan isi kode dalam method dengan `return studentCourseRepository.findAll()` karena memiliki fungsi yang sama tanpa memerlukan loop yang berlebih. Selanjutnya saya kembali menganalisis method method lain yang memakan waktu running yang banyak juga seperti `findStudentWithHighestGPA()` dan juga `joinStudentNames()`. Setelah dioptimisasi, saya run kembali profiler dan melihat running time method-method tersebut sudah berkurang. Kemudian cara saya untuk memastikan tidak ada yang berubah dari segi fungsional adalah saya mencoba menjalankan method2 tersebut dan mengecek hasilnya apakah sama dengan yang lama atau berbeda. Namun, best practice nya sebenarnya adalah dengan melakukan testing di sebelum dan juga sesudah optimization agar memastikan tidak ada fungsionalitas yang berubah sama sekali.

---
## JMeter Test via CMD:
### all-student test
- Before optimization:
```
timeStamp,elapsed,label,responseCode,responseMessage,threadName,dataType,success,failureMessage,bytes,sentBytes,grpThreads,allThreads,URL,Latency,IdleTime,Connect
1741759138280,74938,all-student-request,200,,Thread Group 1 1-3,text,true,,2963150,130,10,10,http://localhost:8080/all-student,74874,0,1
1741759138479,74791,all-student-request,200,,Thread Group 1 1-5,text,true,,2963150,130,9,9,http://localhost:8080/all-student,74769,0,1
1741759138205,75191,all-student-request,200,,Thread Group 1 1-1,text,true,,2963150,130,8,8,http://localhost:8080/all-student,75173,0,37
1741759138206,75311,all-student-request,200,,Thread Group 1 1-2,text,true,,2963150,130,7,7,http://localhost:8080/all-student,75290,0,37
1741759138680,74858,all-student-request,200,,Thread Group 1 1-7,text,true,,2963150,130,6,6,http://localhost:8080/all-student,74841,0,0
1741759138380,75179,all-student-request,200,,Thread Group 1 1-4,text,true,,2963150,130,5,5,http://localhost:8080/all-student,75161,0,1
1741759138580,75024,all-student-request,200,,Thread Group 1 1-6,text,true,,2963150,130,4,4,http://localhost:8080/all-student,75012,0,1
1741759138979,74724,all-student-request,200,,Thread Group 1 1-10,text,true,,2963150,130,3,3,http://localhost:8080/all-student,74704,0,1
1741759138878,74832,all-student-request,200,,Thread Group 1 1-9,text,true,,2963150,130,2,2,http://localhost:8080/all-student,74815,0,1
1741759138779,74946,all-student-request,200,,Thread Group 1 1-8,text,true,,2963150,130,1,1,http://localhost:8080/all-student,74930,0,1
```
- After Optimization:
```
timeStamp,elapsed,label,responseCode,responseMessage,threadName,dataType,success,failureMessage,bytes,sentBytes,grpThreads,allThreads,URL,Latency,IdleTime,Connect
1741762801168,6653,all-student-request,200,,Thread Group 1 1-1,text,true,,2963150,130,10,10,http://localhost:8080/all-student,6599,0,48
1741762801168,6653,all-student-request,200,,Thread Group 1 1-2,text,true,,2963150,130,10,10,http://localhost:8080/all-student,6599,0,48
1741762801431,6579,all-student-request,200,,Thread Group 1 1-5,text,true,,2963150,130,8,8,http://localhost:8080/all-student,6547,0,1
1741762801530,6705,all-student-request,200,,Thread Group 1 1-6,text,true,,2963150,130,7,7,http://localhost:8080/all-student,6672,0,2
1741762801232,7103,all-student-request,200,,Thread Group 1 1-3,text,true,,2963150,130,6,6,http://localhost:8080/all-student,7072,0,1
1741762801829,6641,all-student-request,200,,Thread Group 1 1-9,text,true,,2963150,130,5,5,http://localhost:8080/all-student,6603,0,2
1741762801330,7184,all-student-request,200,,Thread Group 1 1-4,text,true,,2963150,130,4,4,http://localhost:8080/all-student,7153,0,5
1741762801928,6675,all-student-request,200,,Thread Group 1 1-10,text,true,,2963150,130,3,3,http://localhost:8080/all-student,6643,0,2
1741762801634,7194,all-student-request,200,,Thread Group 1 1-7,text,true,,2963150,130,2,2,http://localhost:8080/all-student,7162,0,6
1741762801730,7171,all-student-request,200,,Thread Group 1 1-8,text,true,,2963150,130,1,1,http://localhost:8080/all-student,7148,0,2
```

### all-student-name test:
- Before Optimization:
```
timeStamp,elapsed,label,responseCode,responseMessage,threadName,dataType,success,failureMessage,bytes,sentBytes,grpThreads,allThreads,URL,Latency,IdleTime,Connect
1741760434341,2948,all-student-name,200,,Thread Group 1-2,text,true,,312052,135,10,10,http://localhost:8080/all-student-name,2903,0,41
1741760434413,2883,all-student-name,200,,Thread Group 1-3,text,true,,312052,135,10,10,http://localhost:8080/all-student-name,2880,0,1
1741760434341,3100,all-student-name,200,,Thread Group 1-1,text,true,,312052,135,8,8,http://localhost:8080/all-student-name,3098,0,41
1741760434513,2971,all-student-name,200,,Thread Group 1-4,text,true,,312052,135,7,7,http://localhost:8080/all-student-name,2969,0,4
1741760434711,2789,all-student-name,200,,Thread Group 1-6,text,true,,312052,135,6,6,http://localhost:8080/all-student-name,2788,0,1
1741760435016,2590,all-student-name,200,,Thread Group 1-9,text,true,,312052,135,5,5,http://localhost:8080/all-student-name,2588,0,4
1741760434611,3003,all-student-name,200,,Thread Group 1-5,text,true,,312052,135,4,4,http://localhost:8080/all-student-name,3001,0,2
1741760435129,2509,all-student-name,200,,Thread Group 1-10,text,true,,312052,135,3,3,http://localhost:8080/all-student-name,2508,0,2
1741760434813,2870,all-student-name,200,,Thread Group 1-7,text,true,,312052,135,2,2,http://localhost:8080/all-student-name,2869,0,2
1741760434913,2790,all-student-name,200,,Thread Group 1-8,text,true,,312052,135,1,1,http://localhost:8080/all-student-name,2789,0,2
```

- After Optimization:
```
timeStamp,elapsed,label,responseCode,responseMessage,threadName,dataType,success,failureMessage,bytes,sentBytes,grpThreads,allThreads,URL,Latency,IdleTime,Connect
1741762847070,239,all-student-name,200,,Thread Group 1-3,text,true,,312052,135,5,5,http://localhost:8080/all-student-name,229,0,1
1741762847016,293,all-student-name,200,,Thread Group 1-1,text,true,,312052,135,5,5,http://localhost:8080/all-student-name,283,0,44
1741762847016,293,all-student-name,200,,Thread Group 1-2,text,true,,312052,135,5,5,http://localhost:8080/all-student-name,283,0,44
1741762847170,193,all-student-name,200,,Thread Group 1-4,text,true,,312052,135,2,2,http://localhost:8080/all-student-name,191,0,6
1741762847267,178,all-student-name,200,,Thread Group 1-5,text,true,,312052,135,2,2,http://localhost:8080/all-student-name,177,0,2
1741762847366,164,all-student-name,200,,Thread Group 1-6,text,true,,312052,135,2,2,http://localhost:8080/all-student-name,163,0,1
1741762847465,159,all-student-name,200,,Thread Group 1-7,text,true,,312052,135,2,2,http://localhost:8080/all-student-name,158,0,1
1741762847564,150,all-student-name,200,,Thread Group 1-8,text,true,,312052,135,2,2,http://localhost:8080/all-student-name,148,0,1
1741762847665,165,all-student-name,200,,Thread Group 1-9,text,true,,312052,135,2,2,http://localhost:8080/all-student-name,164,0,1
1741762847764,171,all-student-name,200,,Thread Group 1-10,text,true,,312052,135,1,1,http://localhost:8080/all-student-name,170,0,2
```

### highest-gpa test:
- Before Optimization:
```
timeStamp,elapsed,label,responseCode,responseMessage,threadName,dataType,success,failureMessage,bytes,sentBytes,grpThreads,allThreads,URL,Latency,IdleTime,Connect
1741760759896,262,highest-gpa,200,,Thread Group 1-3,text,true,,266,130,5,5,http://localhost:8080/highest-gpa,256,0,1
1741760759819,339,highest-gpa,200,,Thread Group 1-1,text,true,,266,130,5,5,http://localhost:8080/highest-gpa,333,0,36
1741760759819,339,highest-gpa,200,,Thread Group 1-2,text,true,,266,130,5,5,http://localhost:8080/highest-gpa,333,0,36
1741760759994,291,highest-gpa,200,,Thread Group 1-4,text,true,,266,130,3,3,http://localhost:8080/highest-gpa,291,0,5
1741760760094,225,highest-gpa,200,,Thread Group 1-5,text,true,,266,130,3,3,http://localhost:8080/highest-gpa,225,0,2
1741760760194,177,highest-gpa,200,,Thread Group 1-6,text,true,,266,130,2,2,http://localhost:8080/highest-gpa,177,0,1
1741760760292,156,highest-gpa,200,,Thread Group 1-7,text,true,,266,130,2,2,http://localhost:8080/highest-gpa,156,0,1
1741760760380,142,highest-gpa,200,,Thread Group 1-8,text,true,,266,130,2,2,http://localhost:8080/highest-gpa,142,0,1
1741760760478,160,highest-gpa,200,,Thread Group 1-9,text,true,,266,130,2,2,http://localhost:8080/highest-gpa,160,0,1
1741760760576,171,highest-gpa,200,,Thread Group 1-10,text,true,,266,130,1,1,http://localhost:8080/highest-gpa,171,0,1
```

- After Optimization:
```
timeStamp,elapsed,label,responseCode,responseMessage,threadName,dataType,success,failureMessage,bytes,sentBytes,grpThreads,allThreads,URL,Latency,IdleTime,Connect
1741762875061,245,highest-gpa,200,,Thread Group 1-3,text,true,,266,130,5,5,http://localhost:8080/highest-gpa,237,0,1
1741762875008,297,highest-gpa,200,,Thread Group 1-1,text,true,,266,130,5,5,http://localhost:8080/highest-gpa,289,0,42
1741762875009,297,highest-gpa,200,,Thread Group 1-2,text,true,,266,130,5,5,http://localhost:8080/highest-gpa,289,0,42
1741762875154,214,highest-gpa,200,,Thread Group 1-4,text,true,,266,130,3,3,http://localhost:8080/highest-gpa,214,0,6
1741762875263,195,highest-gpa,200,,Thread Group 1-5,text,true,,266,130,3,3,http://localhost:8080/highest-gpa,195,0,1
1741762875356,193,highest-gpa,200,,Thread Group 1-6,text,true,,266,130,2,2,http://localhost:8080/highest-gpa,193,0,1
1741762875448,184,highest-gpa,200,,Thread Group 1-7,text,true,,266,130,2,2,http://localhost:8080/highest-gpa,184,0,1
1741762875557,194,highest-gpa,200,,Thread Group 1-8,text,true,,266,130,2,2,http://localhost:8080/highest-gpa,194,0,1
1741762875650,196,highest-gpa,200,,Thread Group 1-9,text,true,,266,130,2,2,http://localhost:8080/highest-gpa,196,0,1
1741762875759,194,highest-gpa,200,,Thread Group 1-10,text,true,,266,130,1,1,http://localhost:8080/highest-gpa,194,0,1
```

---
## JMeter Test Via App
### all-student Test:
- Before Optimization:
![WhatsApp Image 2025-03-13 at 12 19 46_81b3b56a](https://github.com/user-attachments/assets/347899a9-20c8-4d78-9b28-26dd0a421ce3)
- After Optimization:
![WhatsApp Image 2025-03-13 at 12 23 29_ccb8a182](https://github.com/user-attachments/assets/7fa338d7-6301-4296-a094-d961e28fca36)

### all-student-name Test:
- Before Optimization:
![WhatsApp Image 2025-03-13 at 12 20 27_ae165991](https://github.com/user-attachments/assets/7a1a6f09-ae99-42d8-b7f6-d687e137d3b8)
- After Optimization:
![WhatsApp Image 2025-03-13 at 12 20 27_ae165991](https://github.com/user-attachments/assets/f3fff3d5-11cc-4db9-abf8-2424efbfddd9)

### highest-gpa Test:
- Before Optimization
![WhatsApp Image 2025-03-13 at 12 24 17_b170cd0b](https://github.com/user-attachments/assets/85429cbc-c717-4173-be2c-63e0ca38d6b7)
- After Optimization:
![WhatsApp Image 2025-03-13 at 12 25 34_9bf43f28](https://github.com/user-attachments/assets/50650004-e8bc-42ae-ad98-7503df59bfc0)


