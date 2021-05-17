# CMake 介紹

在介紹 cmake 之前，必須先介紹c語言在Linux如何被編譯。

![C程式編譯流程](https://1.bp.blogspot.com/-Kx2OqbEB7eM/WSEwMO4b_6I/AAAAAAAAH4k/vAXOHrR4MCsnniai1QITJBYEoT6wCovlACLcB/s1600/C%25E7%25A8%258B%25E5%25BC%258F%25E7%25B7%25A8%25E8%25AD%25AF%25E6%25B5%2581%25E7%25A8%258B.png)



__Preprocessing__ 

 即將 #define 刪除，展開所有巨集。將所有 #include 的檔案插入。處理 #if/#ifdef 等的 conditional 指令。刪除所有註解。添加行號。preprocessing 完後會產生 .i 檔



__Compilation__

_該階段編譯器會檢測程式碼中的錯誤，絕大多數的錯誤和警告產生在這個過程中_

編譯過程就是對預處理完的檔案進行一系列的詞法分析，語法分析，語義分析及優化後生成相應的彙編程式碼。compilation 完後即會產生組合語言碼



__Assembly__

將彙編程式碼轉換為機器指令(二進位制指令)，也就是從 xxx.s 變成 xxx.o。並且會生成符號表，依賴編譯階段的符號彙總，會給每一個符號分配一個地址，所以程式碼中的全域性變數、靜態變數會在該階段分配好儲存空間。



__Linking__

則是將程式所有會用到的 .o 檔做連結。由於 .o 檔是個別編譯的，因此在 .o 檔中並沒有參考到其它 .o 檔變數或函式的真正位址。linker 的目的除了連結所有 .o 檔，也會計算出每個變數或函式的真正位址，然後將所有參考到這些變數或函式的地方填上這個位址。這個動作就叫做 relocation。linking 完後最後就會產生執行檔



## 使用gcc進行編譯



### 連結外部函式庫
到 `/image`的資料夾，在這個範例程式中我`#include<opencv2/opencv.hpp>` ，當要編譯這支程式時就必須連結外部函式庫，執行以下指令

```shell
g++ image.cpp -o image2 -I/usr/include/opencv4/opencv -I/usr/include/opencv4 -lopencv_stitching -lopencv_aruco -lopencv_bgsegm -lopencv_bioinspired -lopencv_ccalib -lopencv_dnn_objdetect -lopencv_dnn_superres -lopencv_dpm -lopencv_highgui -lopencv_face -lopencv_freetype -lopencv_fuzzy -lopencv_hdf -lopencv_hfs -lopencv_img_hash -lopencv_line_descriptor -lopencv_quality -lopencv_reg -lopencv_rgbd -lopencv_saliency -lopencv_shape -lopencv_stereo -lopencv_structured_light -lopencv_phase_unwrapping -lopencv_superres -lopencv_optflow -lopencv_surface_matching -lopencv_tracking -lopencv_datasets -lopencv_text -lopencv_dnn -lopencv_plot -lopencv_ml -lopencv_videostab -lopencv_videoio -lopencv_viz -lopencv_ximgproc -lopencv_video -lopencv_xobjdetect -lopencv_objdetect -lopencv_calib3d -lopencv_imgcodecs -lopencv_features2d -lopencv_flann -lopencv_xphoto -lopencv_photo -lopencv_imgproc -lopencv_core
```

又或者透過pkg-config 指令取得opencv 編譯所需要的參數，進行編譯

```shell
g++ image.cpp -o image2 `pkg-config --cflags --libs opencv4`
```

當在終端機輸入`pkg-config --cflags --libs opencv4`可以發現以下輸出

```shell
$ pkg-config --cflags --libs opencv4
-I/usr/include/opencv4/opencv -I/usr/include/opencv4 -lopencv_stitching -lopencv_aruco -lopencv_bgsegm -lopencv_bioinspired -lopencv_ccalib -lopencv_dnn_objdetect -lopencv_dnn_superres -lopencv_dpm -lopencv_highgui -lopencv_face -lopencv_freetype -lopencv_fuzzy -lopencv_hdf -lopencv_hfs -lopencv_img_hash -lopencv_line_descriptor -lopencv_quality -lopencv_reg -lopencv_rgbd -lopencv_saliency -lopencv_shape -lopencv_stereo -lopencv_structured_light -lopencv_phase_unwrapping -lopencv_superres -lopencv_optflow -lopencv_surface_matching -lopencv_tracking -lopencv_datasets -lopencv_text -lopencv_dnn -lopencv_plot -lopencv_ml -lopencv_videostab -lopencv_videoio -lopencv_viz -lopencv_ximgproc -lopencv_video -lopencv_xobjdetect -lopencv_objdetect -lopencv_calib3d -lopencv_imgcodecs -lopencv_features2d -lopencv_flann -lopencv_xphoto -lopencv_photo -lopencv_imgproc -lopencv_core

```



