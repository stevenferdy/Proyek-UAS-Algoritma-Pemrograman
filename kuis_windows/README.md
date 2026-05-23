# Platform Kuis Online — Versi Windows (Winsock2)
Tugas Akhir Algoritma dan Pemrograman | Teknik Komputer UI

## Perbedaan dari Versi Linux
| Linux                  | Windows (Winsock2)         |
|------------------------|----------------------------|
| `#include <sys/socket>`| `#include <winsock2.h>`    |
| `int socket_fd`        | `SOCKET socket_fd`         |
| `close(sock)`          | `closesocket(sock)`        |
| `g++ ... -pthread`     | `g++ ... -pthread -lws2_32`|
| Tidak perlu init       | `WSAStartup()` wajib       |

## Prasyarat
Install **MinGW** atau **MSYS2** agar punya g++ di Windows:
- Download: https://www.msys2.org
- Setelah install MSYS2, buka MSYS2 terminal dan jalankan:
  ```
  pacman -S mingw-w64-x86_64-gcc
  ```
- Tambahkan `C:\msys64\mingw64\bin` ke PATH Windows

## Cara Menjalankan

### Cara 1 — Double klik file .bat (Paling Mudah)
1. Double klik `run_server.bat` → tunggu server jalan
2. Double klik `run_client.bat` di jendela baru → ikuti kuis
3. Untuk peserta ke-2, 3, dst → double klik `run_client.bat` lagi

### Cara 2 — Manual lewat Command Prompt
```
# Kompilasi server
cd server
g++ -std=c++17 -pthread -I../common main_server.cpp -o server.exe -lws2_32
server.exe

# Kompilasi client (Command Prompt baru)
cd client
g++ -std=c++17 -pthread -I../common main_client.cpp -o client.exe -lws2_32
client.exe
```

## Struktur File
```
quizapp_windows/
├── common/
│   ├── Question.h        ← Abstract Base Class (Abstraksi)
│   ├── QuestionTypes.h   ← MC, TrueFalse, Essay (Inheritance)
│   ├── Participant.h     ← Data peserta + skor (Enkapsulasi)
│   ├── LinkedList.h      ← Manual Linked List (Bonus)
│   ├── Algorithms.h      ← Merge Sort, Quick Sort, Binary/Linear Search
│   └── JsonParser.h      ← JSON serializer
├── server/
│   ├── QuizServer.h      ← Server Winsock2 + Multithreading
│   └── main_server.cpp
├── client/
│   └── main_client.cpp   ← Client Winsock2
├── run_server.bat         ← Double klik untuk jalankan server
└── run_client.bat         ← Double klik untuk jalankan client
```

## Akun & Soal Default
- 9 soal: 4 Multiple Choice, 3 True/False, 2 Essay
- Tambah soal di server/QuizServer.h → fungsi initQuestions()
