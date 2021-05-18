## ex3

本範例示範，利用資料夾拆開，`lib function`跟 `main function` 

從`ex3/lib/CMakeLists.txt`

```cmake
cmake_minimum_required(VERSION 3.2)
project(calc)
add_library(calc calc.cpp)
```

- 其中`project(calc)`指定project名稱，之後可以作為參考變數
- `add_library(<name> [<source> .....])` 可以將程式做成函式庫，做完就會變成`lib<name>.a`

