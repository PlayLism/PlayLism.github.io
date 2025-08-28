---
layout: post
title:  "Panasonic UB820 改全區教學"
date:   2025-08-19 17:16:13 +0800
categories: av
---
![UB820 region free success](https://pub-8c1ddb5aa2ec46d28f40b4295cf14b39.r2.dev/2025/08/6c763da12fbb2c3d12db79aff94beece.jpeg)

早幾個月買入 Panasonic UB820 UHD 藍光機，當時試過改全區但不成功，早前見到軟改全區方案有更新，終於成功。 

> 以下教學參考此兩個教學： 
> - [AVForums][avforums]
> - [MovieSide][movieside]

### 事前準備： 

1. 藍光機需要先升級為 1.82 版原裝系統，可以直接上網升級。 
> Setup -> Player Settings -> System -> Firmware Update -> Update Now 

2. 建議先重設系統並關閉 Quick Start 及 VIERA Link。 
> Setup -> Player Settings -> System -> Default Settings 
> Player Settings -> System -> Quick Start -> Off 
> Player Settings -> System -> TV Settings -> VIERA Link -> Off 

3. 建議在改全區時連接 LAN 線而不要用 WiFi，接駁 LAN 線後要再設定連線方式，並且記錄 IP 地址，後來的過程要輸入這 IP 地址。 
> Setup -> Player Settings -> Network -> Easy Network Setting -> Wired
> Setup -> Player Settings -> Network -> Network Settings -> IP Address / DNS Settings 

4. 改全區過程時不能有光碟或改機檔 USB 以外的 USB 裝置。 

5. 準備 8GB 或以上的 USB 儲存裝置。 

### 改全區過程： 

1.  [安裝 Oracle VirtualBox][virtualbox]、[下載已經安裝好所需元件的 Linux 虛擬機][vm-link]，雖然你亦可以自行在 Linux 系統中安裝所需元件，但直接用依個虛擬機就可以減少麻煩。下載後運行lubuntu.vbox。如果以下過程需要密碼，請輸入 **lulu** 。 

2. 在 Linux 中使用 Firefox [下載改全區軟件 "Patch-Program169-182"][patch-program-link] 並解壓縮。 

3. [下載新版 `drive.img.gz`][new-drive-img-link] 並替換 `Patch-Program169-182\res` 資料夾中的同名檔案。 

4. 插入 USB 儲存裝置並在 VirtualBox 中掛載，成功掛載後會在 Linux 系統中出現 `Open in File Manager` 的視窗。 
> Devices -> USB -> `USB 裝置的名稱` 

5. 在 `Patch-Program169-182` 資料夾中運行 `Patcher`。 

6. 在 `Patcher` 程式的右上角按 `Select USB Device` 並選擇你的USB 儲存裝置，再次確定後就會開始寫入改機檔。 

7. 在檔案管理員中按退出圖示將 USB 儲存裝置移除。 

8. 將藍光機關機，插入有改機檔的 USB 儲存裝置，然後開機。 

9. 見到藍光機進入主頁畫面後，在 `Patcher` 的左上方輸入藍光機的 IP 地址並按 "Connect"。 

10. 連接成功後按 `Exec Script`，這步驟會備份藍光機的系統到 USB 儲存裝置中。 

11. 見到程式出現 `- ALL DONE` 字樣後，把藍光機關機並移除 USB 儲存裝置。 

12. 將 USB 儲存裝置插回電腦並掛載，在檔案管理員中選擇容量較大的 Volume，確定有 `script.sh`、`fma4.img`、`fma5.img`、`fma6.img` 及 `fma7.img`。在檔案管理員上方的地址欄複製 USB 儲存裝置的路徑 (格式為 `XXXX-XXXX`)。 

13. 在桌面開啟 `Qterminal`，並輸入 
> cd /media/lu/`USB 儲存裝置的路徑`

14. 輸入 `dir` 確定見到 `script.sh` 等檔案。 

15. 輸入 `sudo bash 2_patch.sh` 去修改藍光機系統檔案，按 Enter 後輸入密碼。

16. 輸入 `cp -f 3_write.sh script.sh`。 

17. 在檔案管理員中按退出圖示將 USB 儲存裝置移除。 

18. 將藍光機關機，插入有改機檔的 USB 儲存裝置，然後開機。 

19. 見到藍光機進入主頁畫面後，在 `Patcher` 的左上方輸入藍光機的 IP 地址並按 `Connect`。 

20. 現在就會開始寫入修改後的系統檔案，過程可能需要 15-20 分鐘，但由於藍光機在主頁停留 20 分鐘後就會自動關機，需要每隔十分鐘按右方向鍵避免它自動關機。 

21. 當見到 "Patcher" 出現 `### ALL DONE ###` 字樣時，將藍光機關機並拔走 USB 儲存裝置及電源線後，約十秒後重新插入電源線再開機。 

22. 開機後會見到 Panasonic 標誌下有 "Region Free" 字樣，代表改機成功。這時候可以把 Linux 虛擬機關機。建議備份 USB 儲存裝置中的 `fma4.img`、`fma5.img`、`fma6.img` 及 `fma7.img`，因為這是未經修改的原系統檔案。 

![UB820 region free patcher success](https://pub-8c1ddb5aa2ec46d28f40b4295cf14b39.r2.dev/2025/08/bc8bb81ecd23bbe577768bc647405af5.jpg)

### 改區碼方法： 

搖控 `OPTION` 鍵按三次 + DVD 區碼 `1-8` + 藍光區碼 `1 = A, 2 = B, 3 = C`，及後就會自動重新開機。

[avforums]: https://www.avforums.com/threads/lets-try-again-to-put-the-free-in-regionfreedom.2441584/post-31906429
[movieside]: https://www.movieside.de/threads/guide-zum-flashen-der-panasonic-codefree-custom-firmware-ub424-ub824-ub9004-update-1-82.22660/
[virtualbox]: https://www.virtualbox.org/wiki/Downloads
[vm-link]: https://mega.nz/file/AllU3DhR#t2pmtamQiXu42ZMcBjvdGnzEvg4OK9M2zNrPKKsSDEs
[patch-program-link]: https://gofile.io/d/3Vd1BT
[new-drive-img-link]: https://mega.nz/file/A8MBwaSL#_fRBNf1op-_q5xeJTXplFPdHFBQPUEK7r80Xz_46W04