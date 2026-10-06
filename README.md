\# Báo cáo Bài 4: Quản lý tiến trình nền với nohup và tín hiệu Kill



\## 1. Nhật ký lệnh thực thi



```bash

\# 1. Tạo file và cấp quyền thực thi

cat << 'EOF' > loop-monitor.sh

\#!/bin/bash

while true; do

&#x20;   echo "System time: $(date)" >> /tmp/monitor.log

&#x20;   sleep 5

done

EOF

chmod +x loop-monitor.sh



\# 2. Chạy nền với nohup

nohup ./loop-monitor.sh > /dev/null 2>\&1 \&



\# 3. Tra cứu PID tiến trình

ps aux | grep loop-monitor.sh



\# 4. Kiểm tra file log

tail -n 5 /tmp/monitor.log



\# 5. Dừng tiến trình bằng SIGTERM

kill -15 <PID\_CUA\_TIEN\_TRINH>



2\. Kết quả kiểm tra tiến trình và file log

Trạng thái chạy nền (ps aux | grep loop-monitor.sh)

Plaintext

root     14523  0.0  0.1  13280  3148 pts/0    S    12:35   0:00 /bin/bash ./loop-monitor.sh

PID của tiến trình: 14523



Nội dung log ghi nhận (tail -n 5 /tmp/monitor.log)

Plaintext

System time: Tue Oct  6 12:35:10 UTC 2026

System time: Tue Oct  6 12:35:15 UTC 2026

System time: Tue Oct  6 12:35:20 UTC 2026

System time: Tue Oct  6 12:35:25 UTC 2026

System time: Tue Oct  6 12:35:30 UTC 2026

3\. Kết quả sau khi gửi tín hiệu kill (kill -15 14523)

Kiểm tra lại tiến trình:



Plaintext

root@lab-practice:\~# ps aux | grep loop-monitor.sh

root     14610  0.0  0.0   6480  2176 pts/0    S+   12:36   0:00 grep --color=auto loop-moni

