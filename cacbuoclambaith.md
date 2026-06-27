BÀI 1: Sơ đồ cây tiến trình (Gõ lệnh tạo sơ đồ chữ
Gõ lệnh mở file:
Bash
nano bai1.txt
Dùng bàn phím gõ chính xác nội dung này vào màn hình
Plaintext
       [ Tien trinh CHA ]
               │
           Lenh fork()
        ┌──────┴──────┐
        ▼             ▼
  [ Tien trinh ]   [ Tien trinh ]
     CHA (A)          CON (B)
Cách lưu: Nhấn Ctrl + O ➜ Nhấn Enter để lưu ➜ Nhấn Ctrl + X để thoát.
Bài 2
Bước 1: Mở file code Bài 2
Gõ lệnh sau để mở trình soạn thảo:
Bash
nano bai2.c
Bước 2: Gõ đoạn code Bài 2 vào màn hình
Bạn gõ chính xác đoạn code đếm dừa này từ file PDF vào máy 
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/wait.h>
int main() {
    pid_t pid;
    int num_coconuts = 17;
    
    pid = fork();
    if (pid == 0) {
        num_coconuts = 42;
        exit(0);
    } else {
        wait(NULL); /* wait until the child terminates */
    }
    
    printf("I see %d coconuts!\n", num_coconuts);
    exit(0);
}
Bước 3: Lưu và Thoát
Nhấn tổ hợp phím Ctrl + O rồi nhấn Enter để lưu file.
Nhấn tổ hợp phím Ctrl + X để thoát ra ngoài Terminal đen.
Bước 4: Biên dịch và Chạy thử 
Gõ 2 lệnh này để chạy chương trình:
Bash
gcc bai2.c -o bai2
./bai2
Kết quả hiện ra màn hình:
Plaintext
I see 17 coconuts!

💻 BÀI 3: Thực thi lệnh ls -l qua fork() và exec()
Gõ lệnh mở file:
Bash
nano bai3.c
Gõ đoạn code chuẩn này vào:
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/wait.h>
int main() {
    pid_t pid = fork();
    if (pid < 0) return 1;
    else if (pid == 0) {
        printf("Tien trinh con thực hien 'ls -l':\n");
        execlp("ls", "ls", "-l", NULL);
        exit(1);
    } else {
        wait(NULL);
        printf("\nTien trinh cha ket thuc!\n");
    }
    return 0;
}
Lưu và thoát: Nhấn Ctrl + O ➜ Enter ➜ Nhấn Ctrl + X.
1.
2.
Biên dịch và chạy thử
Bash
gcc bai3.c -o bai3
./bai3
⏱️ BÀI 4: Đo thời gian thực thi một lệnh bất kỳ
Gõ lệnh mở file:
Bash
nano bai4.c
Gõ đoạn code đo thời gian này vào
#include <stdio.h> 
#include <stdlib.h>#
include <unistd.h>
#include <sys/wait.h>
#include <sys/time.h>
int main(int argc, char *argv[]) {
    if (argc < 2) return 1;
    struct timeval start, end;
    gettimeofday(&start, NULL);
    if (fork() == 0) {
        execvp(argv[1], &argv[1]);
        exit(1);
    } else {
        wait(NULL);
        gettimeofday(&end, NULL);
        double time = (end.tv_sec - start.tv_sec) + (end.tv_usec - start.tv_usec) / 1000000.0;
        printf("\n[Thoi gian thuc thi: %.6f giay]\n", time);
    }
    return 0;
}
Lưu và thoát: Nhấn Ctrl + O ➜ Enter ➜ Nhấn Ctrl + X.
Biên dịch và chạy thử với lệnh ls:
Bash
gcc bai4.c -o bai4
./bai4 ls
