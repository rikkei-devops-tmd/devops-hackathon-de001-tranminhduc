DEVOPS HACKATHON - DE 001: QUAN LY PHONG LAB

1. THONG TIN SINH VIEN
- Ho va ten: Tran Minh Duc
- Ma sinh vien: K24CNTT1
- Lop: K24-CNTT1
- Tai khoan Linux: tranminhduc-k24cntt1
- GitHub: rikkei-devops-tmd
- Cong Nginx: 8088

2. MOI TRUONG TRIEN KHAI
- He dieu hanh: Ubuntu 24.04 LTS (x86_64)
- Phien ban Nginx: 1.24+
- Phien ban Git: 2.43+
- Noi chay: VPS Cloud Linux (IP: 103.20.102.126)

3. CAU TRUC DU AN
devops-hackathon-de001-tranminhduc/
src/ index.html
nginx/
   tranminhduc-k24cntt1.conf
screenshots/
        01-user.png 
        02-nginx.png
        03-ufw.png
        04-website.png
        05-git-log.png
        06-update.png 
.gitignore
README.md

4. CAU HINH NGINX
- <PORT>: 8088 (Cong ca nhan phuc vu website qua Nginx IPv4 va IPv6)
- <SERVER_NAME>: 103.20.102.126 (Dia chi IP may chu VPS phuc vu request)
- <WEB_ROOT>: /var/www/devops-hackathon-de001-tranminhduc/src (Duong dan tuyet doi tro vao web root)
- <INDEX_FILE>: index.html (Tep tin trang chu mac dinh)
- <TEN_TAI_KHOAN>: tranminhduc-k24cntt1 (Ten tai khoan Linux dung dat ten file access va error log)
- <ALLOW_DIRECTIVE>: allow all; (Chi thi Nginx cho phep moi truy cap HTTP tu ben ngoai)

5. TUONG LUA UFW
Cac rule da cau hinh:
- 22/tcp (SSH - quan tri tu xa)
- 8088/tcp (Nginx - truy cap website tu Internet)

Ket qua lenh sudo ufw status verbose:
Status: active
Logging: on (low)
Default: deny (incoming), allow (outgoing), disabled (routed)
New profiles: skip

To                         Action      From
--                         ------      ----
22/tcp                     ALLOW IN    Anywhere
8088/tcp                   ALLOW IN    Anywhere
22/tcp (v6)                ALLOW IN    Anywhere (v6)
8088/tcp (v6)              ALLOW IN    Anywhere (v6)

6. CAC BUOC TRIEN KHAI
1. Khoi tao nguoi dung: sudo adduser tranminhduc-k24cntt1 va cap quyen: sudo usermod -aG sudo tranminhduc-k24cntt1.
2. Cai dat goi phan mem: sudo apt update && sudo apt install -y nginx git ufw curl.
3. Cau hinh Git danh tinh: git config --global user.name "Tran Minh Duc" va git config --global user.email "tranminhduc@example.com".
4. Clone ma nguon tu GitHub: sudo git clone https://github.com/rikkei-devops-tmd/devops-hackathon-de001-tranminhduc.git /var/www/devops-hackathon-de001-tranminhduc.
5. Phan quyen chuan: sudo chown -R tranminhduc-k24cntt1:tranminhduc-k24cntt1 /var/www/devops-hackathon-de001-tranminhduc, cap quyen thu muc 755 va tep tin 644.
6. Kich hoat Server Block Nginx:
- sudo cp /var/www/devops-hackathon-de001-tranminhduc/nginx/tranminhduc-k24cntt1.conf /etc/nginx/sites-available/
- sudo ln -s /etc/nginx/sites-available/tranminhduc-k24cntt1.conf /etc/nginx/sites-enabled/
- sudo rm -f /etc/nginx/sites-enabled/default
7. Kiem tra va tai lai Nginx: sudo nginx -t && sudo systemctl reload nginx.
8. Thiet lap tuong lua UFW: sudo ufw allow 22/tcp && sudo ufw allow 8088/tcp && sudo ufw --force enable.

7. KIEM TRA VA MINH CHUNG
- Minh chung 1: 01-user.png (Ket qua lenh id va whoami cua tai khoan tranminhduc-k24cntt1)
- Minh chung 2: 02-nginx.png (Ket qua sudo nginx -t va sudo systemctl status nginx)
- Minh chung 3: 03-ufw.png (Ket qua sudo ufw status verbose the hien mo cong 8088)
- Minh chung 4: 04-website.png (Trinh duyet mo http://103.20.102.126:8088 hien thi trang web sinh vien)
- Minh chung 5: 05-git-log.png (Lich su commit git log --oneline the hien du cac commit)
- Minh chung 6: 06-update.png (Giao dien website sau khi cap nhat noi dung lan 2)

8. QUY TRINH CAP NHAT WEBSITE
1. Tren may tinh ca nhan: Chinh sua file src/index.html (them thong tin Cap nhat lan 2).
2. Commit va day len GitHub:
git add src/index.html
git commit -m "feat: Cap nhat noi dung website lan 2"
git push origin main
3. Tren may chu Linux: Di chuyen vao thu muc du an va keo ma nguon moi:
cd /var/www/devops-hackathon-de001-tranminhduc
git pull origin main
4. Nghiem thu: Trang web tu dong hien thi noi dung moi ngay lap tuc ma khong can reload dich vu Nginx.

9. SU CO GAP PHAI VA CACH KHAC PHUC
1. Su co phan quyen khi git pull:
- Hien tuong: Thu muc duoc clone ban dau boi root khien tai khoan sinh vien khong co quyen ghi de khi chay git pull.
- Khac phuc: Thuc hien sudo chown -R tranminhduc-k24cntt1:tranminhduc-k24cntt1 /var/www/devops-hackathon-de001-tranminhduc de trao toan quyen so huu cho tai khoan lam viec.
2. Tranh xung dot cong mang tren may chu dung chung:
- Hien tuong: Cong 80 mac dinh bi chiem dung boi nhieu dich vu hoac bai thi khac.
- Khac phuc: Tach biet hoan toan sang cong rieng 8088, cau hinh Nginx Server Block doc lap va mo cong tuong ung tren tuong lua UFW.