準備一台x86設備，並安裝Ubuntu18.04以上的系統，磁片可用空間大於30G,若使用SDKmanager安裝CUDA等庫，則需要磁片可用空間大於50G 
1.	打開https://developer.nvidia.com/embedded/linux-tegra-r3251 
 
2.	下載BSP文件和跟檔案系統： 
  ![image](https://github.com/mark-nexcom/3501/assets/63223264/44cef915-db37-4066-9341-d58d7b58329d)

3.	拷貝提供的其它檔到與第二步下載的位置同一資料夾下（如果提供的檔中中有system.img,資料夾所在的分區可用空間能夠放下這些檔即可，否則該分區的可用空間需要大於30G） 
4.	解壓下載的L4T Driver Package(BSP)檔（BSP檔所在位置打開終端，解壓檔，不需要使用sudo）：tar -xvf xxx 
5.	拷貝Sample Root Filesystem檔到4步解壓的資料夾Linux_for_Tegra/rootfs/下，打開終端，解壓該檔（需要使用sudo）:sudo tar -xvf xxxx 
6.	在Linux_for_Tegra下打開終端，執行sudo ./apply_binaries.sh 
7.	替換檔，將我司提供的相關檔放到第4步解壓的資料夾中的相應位置： 
內核Image -> Linux_for_Tegra/kernel/ 
設備樹tegra186-p3636-0001-p3509-0000-a01.dtb -> Linux_for_Tegra/kernel/dtb/ 
Pinmux tegra186-mb1-bct-pinmux-p3636-0001-a00.cfg -> Linux_for_Tegra/bootloader/t186ref/BCT/ 
8.	將coeus產品進入到復原模式並與主機通過OTG口與主機連接，在Linux_for_Tegra下執行如下燒錄命令，燒錄完畢終端提示燒錄成功，設備將自動重啟（部分不重啟需要手動斷電後重新上電） 
3601系列： 
重構：sudo ./flash.sh jetson-xavier-nx-devkit-tx2-nx mmcblk0p1 
不重構：sudo ./flash.sh –no-systemimg jetson-xavier-nx-devkit-tx2-nx mmcblk0p1 
提示：不提供system.img需要重構（該過程耗時，第一次重構後，後面可以不用重構），提供xxx.img鏡像選擇不重構, 並把xxx.img鏡像放到Linux_for_Tegra/bootloader/下，命名為：system.img 
9.	Audio 設置： 
將alsa-cmd_lout_tx2nx.sh檔拷貝到coeus中，並在該檔所在的目錄下打開終端執行如下命令： 
sudo chmod +x alsa-cmd_lout_tx2nx.sh 
sudo ./alsa-cmd_lout_tx2nx.sh 
插入耳機，播放音訊，能聽到聲音則證明設置成功 
 

