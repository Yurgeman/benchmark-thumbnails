# Thumbnails benchmark

Test PC - **AWS t3.small**:
```
$ free -h
              total        used        free      shared  buff/cache   available
Mem:          1.9Gi       250Mi       715Mi       1.0Mi       1.0Gi       1.5Gi
Swap:            0B          0B          0B
```
```
$ lscpu
Architecture:                    x86_64
CPU op-mode(s):                  32-bit, 64-bit
Byte Order:                      Little Endian
Address sizes:                   46 bits physical, 48 bits virtual
CPU(s):                          2
On-line CPU(s) list:             0,1
Thread(s) per core:              2
Core(s) per socket:              1
Socket(s):                       1
NUMA node(s):                    1
Vendor ID:                       GenuineIntel
CPU family:                      6
Model:                           85
Model name:                      Intel(R) Xeon(R) Platinum 8259CL CPU @ 2.50GHz
Stepping:                        7
CPU MHz:                         2499.996
BogoMIPS:                        4999.99
Hypervisor vendor:               KVM
Virtualization type:             full
L1d cache:                       32 KiB
L1i cache:                       32 KiB
L2 cache:                        1 MiB
L3 cache:                        35.8 MiB
NUMA node0 CPU(s):               0,1
Vulnerability Itlb multihit:     KVM: Mitigation: VMX unsupported
Vulnerability L1tf:              Mitigation; PTE Inversion
Vulnerability Mds:               Vulnerable: Clear CPU buffers attempted, no microcode; SMT Host state unknown
Vulnerability Meltdown:          Mitigation; PTI
Vulnerability Spec store bypass: Vulnerable
Vulnerability Spectre v1:        Mitigation; usercopy/swapgs barriers and __user pointer sanitization
Vulnerability Spectre v2:        Mitigation; Full generic retpoline, STIBP disabled, RSB filling
Vulnerability Srbds:             Not affected
Vulnerability Tsx async abort:   Not affected
Flags:                           fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush mmx fxsr sse sse2 ss
                                 ht syscall nx pdpe1gb rdtscp lm constant_tsc rep_good nopl xtopology nonstop_tsc cpuid tsc_known_freq
                                  pni pclmulqdq ssse3 fma cx16 pcid sse4_1 sse4_2 x2apic movbe popcnt tsc_deadline_timer aes xsave avx
                                  f16c rdrand hypervisor lahf_lm abm 3dnowprefetch invpcid_single pti fsgsbase tsc_adjust bmi1 avx2 sm
                                 ep bmi2 erms invpcid mpx avx512f avx512dq rdseed adx smap clflushopt clwb avx512cd avx512bw avx512vl
                                 xsaveopt xsavec xgetbv1 xsaves ida arat pku ospke
```


|             | imgproxy                  | thumbor                   | thumbor (with `file_storage` cache) | imaginary                  | picfit                    | picfit (with `fs` cache)  | imageproxy                | imageproxy (with `in memory` cache) |
| ----------- | ------------------------- | ------------------------- | ----------------------------------- | -------------------------- | ------------------------- | ------------------------- | --------------------------| ----------------------------------- |
| 320x240     | 71.90ms (14.02 rps, 60MB) | 90.51ms (11.09 rps, 60MB) | 1.79ms (893.27 rps, 50MB)           | 69.55ms (14.48 rps, 200MB) | 238.91ms (4.18 rps, 50MB) | 8.23ms (922.42 rps, 40MB) | 226.29ms (4.41 rps, 60MB) | 2.41ms (3207.52 rps, 40MB)          |
| 854x480     | 105.17ms (9.55 rps, 65MB) | 84.06ms (11.93 rps, 65MB) | 1.33ms (754.58 rps, 50MB)           | 89.84ms (11.19 rps, 320MB) | 303.05ms (3.29 rps, 60MB) | 4.56ms (490.97 rps, 40MB) | 295.18ms (3.38 rps, 70MB) | 1.63ms (1998.03 rps, 40MB)          |
| 1280x720    | 168.57ms (5.94 rps, 70MB) | 186.55ms (5.34 rps, 70MB) | 2.24ms (595.12 rps, 50MB)           | 104.65ms (9.58 rps, 380MB) | 345.35ms (2.88 rps, 65MB) | 6.31ms (320.05 rps, 40MB) | 373.96ms (2.68 rps, 80MB) | 2.40ms (1296.11 rps, 40MB)          |


![https://quickchart.io/sandbox/#%7B%0A%20%20%22type%22%3A%20%22horizontalBar%22%2C%0A%20%20%22data%22%3A%20%7B%0A%20%20%20%20%22labels%22%3A%20%5B%0A%20%20%20%20%20%20%22imgproxy%22%2C%0A%20%20%20%20%20%20%22thumbor%22%2C%0A%20%20%20%20%20%20%22thumbor%20(with%20cache)%22%2C%0A%20%20%20%20%20%20%22imaginary%22%2C%0A%20%20%20%20%20%20%22picfit%22%2C%0A%20%20%20%20%20%20%22picfit%20(with%20cache)%22%2C%0A%20%20%20%20%20%20%22imageproxy%22%2C%0A%20%20%20%20%20%20%22imageproxy%20(with%20cache)%22%2C%0A%20%20%20%20%5D%2C%0A%20%20%20%20%22datasets%22%3A%20%5B%0A%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%22label%22%3A%20%22320x240%22%2C%0A%20%20%20%20%20%20%20%20%22backgroundColor%22%3A%20%22rgba(54%2C%20162%2C%20235%2C%200.5)%22%2C%0A%20%20%20%20%20%20%20%20%22borderColor%22%3A%20%22rgb(54%2C%20162%2C%20235)%22%2C%0A%20%20%20%20%20%20%20%20%22borderWidth%22%3A%201%2C%0A%20%20%20%20%20%20%20%20%22data%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%2071.90%2C%0A%20%20%20%20%20%20%20%20%20%2090.51%2C%0A%20%20%20%20%20%20%20%20%20%201.79%2C%0A%20%20%20%20%20%20%20%20%20%2069.55%2C%0A%20%20%20%20%20%20%20%20%20%20238.91%2C%0A%20%20%20%20%20%20%20%20%20%208.23%2C%0A%20%20%20%20%20%20%20%20%20%20226.29%2C%0A%20%20%20%20%20%20%20%20%20%202.41%2C%0A%20%20%20%20%20%20%20%20%5D%0A%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%22label%22%3A%20%22854x480%22%2C%0A%20%20%20%20%20%20%20%20%22backgroundColor%22%3A%20%22rgba(255%2C%2099%2C%20132%2C%200.5)%22%2C%0A%20%20%20%20%20%20%20%20%22borderColor%22%3A%20%22rgb(255%2C%2099%2C%20132)%22%2C%0A%20%20%20%20%20%20%20%20%22borderWidth%22%3A%201%2C%0A%20%20%20%20%20%20%20%20%22data%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20105.17%2C%0A%20%20%20%20%20%20%20%20%20%2084.06%2C%0A%20%20%20%20%20%20%20%20%20%201.33%2C%0A%20%20%20%20%20%20%20%20%20%2089.84%2C%0A%20%20%20%20%20%20%20%20%20%20303.05%2C%0A%20%20%20%20%20%20%20%20%20%204.56%2C%0A%20%20%20%20%20%20%20%20%20%20295.18%2C%0A%20%20%20%20%20%20%20%20%20%201.63%2C%0A%20%20%20%20%20%20%20%20%5D%0A%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%22label%22%3A%20%221280x720%22%2C%0A%20%20%20%20%20%20%20%20%22backgroundColor%22%3A%20%22rgb(201%2C%20203%2C%20207)%22%2C%0A%20%20%20%20%20%20%20%20%22borderColor%22%3A%20%22rgb(154%2C%20162%2C%20235)%22%2C%0A%20%20%20%20%20%20%20%20%22borderWidth%22%3A%201%2C%0A%20%20%20%20%20%20%20%20%22data%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20168.57%2C%0A%20%20%20%20%20%20%20%20%20%20186.55%2C%0A%20%20%20%20%20%20%20%20%20%202.24%2C%0A%20%20%20%20%20%20%20%20%20%20104.65%2C%0A%20%20%20%20%20%20%20%20%20%20345.35%2C%0A%20%20%20%20%20%20%20%20%20%206.31%2C%0A%20%20%20%20%20%20%20%20%20%20373.96%2C%0A%20%20%20%20%20%20%20%20%20%202.40%2C%0A%20%20%20%20%20%20%20%20%5D%0A%20%20%20%20%20%20%7D%0A%20%20%20%20%5D%0A%20%20%7D%2C%0A%20%20%22options%22%3A%20%7B%0A%20%20%20%20%22plugins%22%3A%20%7B%0A%20%20%20%20%20%20%22datalabels%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22anchor%22%3A%20%22end%22%2C%0A%20%20%20%20%20%20%20%20%22align%22%3A%20%22end%22%2C%0A%20%20%20%20%20%20%20%20%22color%22%3A%20%22%23000%22%0A%20%20%20%20%20%20%7D%0A%20%20%20%20%7D%2C%0A%20%20%20%20%22responsive%22%3A%20true%2C%0A%20%20%20%20%22legend%22%3A%20%7B%0A%20%20%20%20%20%20%22position%22%3A%20%22top%22%0A%20%20%20%20%7D%2C%0A%20%20%20%20%22title%22%3A%20%7B%0A%20%20%20%20%20%20%22display%22%3A%20true%2C%0A%20%20%20%20%20%20%22text%22%3A%20%22Rendering%20time%20in%20milliseconds%20(lower%20is%20better)%22%0A%20%20%20%20%7D%0A%20%20%7D%0A%7D](https://quickchart.io/chart?w=900&h=500&c=%7B%0A%20%20%22type%22%3A%20%22horizontalBar%22%2C%0A%20%20%22data%22%3A%20%7B%0A%20%20%20%20%22labels%22%3A%20%5B%0A%20%20%20%20%20%20%22imgproxy%22%2C%0A%20%20%20%20%20%20%22thumbor%22%2C%0A%20%20%20%20%20%20%22thumbor%20(with%20cache)%22%2C%0A%20%20%20%20%20%20%22imaginary%22%2C%0A%20%20%20%20%20%20%22picfit%22%2C%0A%20%20%20%20%20%20%22picfit%20(with%20cache)%22%2C%0A%20%20%20%20%20%20%22imageproxy%22%2C%0A%20%20%20%20%20%20%22imageproxy%20(with%20cache)%22%2C%0A%20%20%20%20%5D%2C%0A%20%20%20%20%22datasets%22%3A%20%5B%0A%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%22label%22%3A%20%22320x240%22%2C%0A%20%20%20%20%20%20%20%20%22backgroundColor%22%3A%20%22rgba(54%2C%20162%2C%20235%2C%200.5)%22%2C%0A%20%20%20%20%20%20%20%20%22borderColor%22%3A%20%22rgb(54%2C%20162%2C%20235)%22%2C%0A%20%20%20%20%20%20%20%20%22borderWidth%22%3A%201%2C%0A%20%20%20%20%20%20%20%20%22data%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%2071.90%2C%0A%20%20%20%20%20%20%20%20%20%2090.51%2C%0A%20%20%20%20%20%20%20%20%20%201.79%2C%0A%20%20%20%20%20%20%20%20%20%2069.55%2C%0A%20%20%20%20%20%20%20%20%20%20238.91%2C%0A%20%20%20%20%20%20%20%20%20%208.23%2C%0A%20%20%20%20%20%20%20%20%20%20226.29%2C%0A%20%20%20%20%20%20%20%20%20%202.41%2C%0A%20%20%20%20%20%20%20%20%5D%0A%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%22label%22%3A%20%22854x480%22%2C%0A%20%20%20%20%20%20%20%20%22backgroundColor%22%3A%20%22rgba(255%2C%2099%2C%20132%2C%200.5)%22%2C%0A%20%20%20%20%20%20%20%20%22borderColor%22%3A%20%22rgb(255%2C%2099%2C%20132)%22%2C%0A%20%20%20%20%20%20%20%20%22borderWidth%22%3A%201%2C%0A%20%20%20%20%20%20%20%20%22data%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20105.17%2C%0A%20%20%20%20%20%20%20%20%20%2084.06%2C%0A%20%20%20%20%20%20%20%20%20%201.33%2C%0A%20%20%20%20%20%20%20%20%20%2089.84%2C%0A%20%20%20%20%20%20%20%20%20%20303.05%2C%0A%20%20%20%20%20%20%20%20%20%204.56%2C%0A%20%20%20%20%20%20%20%20%20%20295.18%2C%0A%20%20%20%20%20%20%20%20%20%201.63%2C%0A%20%20%20%20%20%20%20%20%5D%0A%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20%22label%22%3A%20%221280x720%22%2C%0A%20%20%20%20%20%20%20%20%22backgroundColor%22%3A%20%22rgb(201%2C%20203%2C%20207)%22%2C%0A%20%20%20%20%20%20%20%20%22borderColor%22%3A%20%22rgb(154%2C%20162%2C%20235)%22%2C%0A%20%20%20%20%20%20%20%20%22borderWidth%22%3A%201%2C%0A%20%20%20%20%20%20%20%20%22data%22%3A%20%5B%0A%20%20%20%20%20%20%20%20%20%20168.57%2C%0A%20%20%20%20%20%20%20%20%20%20186.55%2C%0A%20%20%20%20%20%20%20%20%20%202.24%2C%0A%20%20%20%20%20%20%20%20%20%20104.65%2C%0A%20%20%20%20%20%20%20%20%20%20345.35%2C%0A%20%20%20%20%20%20%20%20%20%206.31%2C%0A%20%20%20%20%20%20%20%20%20%20373.96%2C%0A%20%20%20%20%20%20%20%20%20%202.40%2C%0A%20%20%20%20%20%20%20%20%5D%0A%20%20%20%20%20%20%7D%0A%20%20%20%20%5D%0A%20%20%7D%2C%0A%20%20%22options%22%3A%20%7B%0A%20%20%20%20%22plugins%22%3A%20%7B%0A%20%20%20%20%20%20%22datalabels%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%22anchor%22%3A%20%22end%22%2C%0A%20%20%20%20%20%20%20%20%22align%22%3A%20%22end%22%2C%0A%20%20%20%20%20%20%20%20%22color%22%3A%20%22%23000%22%0A%20%20%20%20%20%20%7D%0A%20%20%20%20%7D%2C%0A%20%20%20%20%22responsive%22%3A%20true%2C%0A%20%20%20%20%22legend%22%3A%20%7B%0A%20%20%20%20%20%20%22position%22%3A%20%22top%22%0A%20%20%20%20%7D%2C%0A%20%20%20%20%22title%22%3A%20%7B%0A%20%20%20%20%20%20%22display%22%3A%20true%2C%0A%20%20%20%20%20%20%22text%22%3A%20%22Rendering%20time%20in%20milliseconds%20(lower%20is%20better)%22%0A%20%20%20%20%7D%0A%20%20%7D%0A%7D)


Tests based on https://github.com/wg/wrk:
```
imgproxy:
    320x240
        ./wrk -t1 -c1 -d60s http://localhost:8080/unsafe/fill/320/240/ce/1/plain/https%3A%2F%2Fraw.githubusercontent.com%2Fmamchyts%2Fbenchmark-thumbnails%2Fmaster%2Fnature-wallpaper-1920x1080.jpg
    854x480
        ./wrk -t1 -c1 -d60s http://localhost:8080/unsafe/fill/854/480/ce/1/plain/https%3A%2F%2Fraw.githubusercontent.com%2Fmamchyts%2Fbenchmark-thumbnails%2Fmaster%2Fnature-wallpaper-1920x1080.jpg
    1280x720
        ./wrk -t1 -c1 -d60s http://localhost:8080/unsafe/fill/1280/720/ce/1/plain/https%3A%2F%2Fraw.githubusercontent.com%2Fmamchyts%2Fbenchmark-thumbnails%2Fmaster%2Fnature-wallpaper-1920x1080.jpg

thumbor:
    320x240
        ./wrk -t1 -c1 -d60s http://localhost:8081/unsafe/320x240/https%3A%2F%2Fraw.githubusercontent.com%2Fmamchyts%2Fbenchmark-thumbnails%2Fmaster%2Fnature-wallpaper-1920x1080.jpg
    854x480
        ./wrk -t1 -c1 -d60s http://localhost:8081/unsafe/854x480/https%3A%2F%2Fraw.githubusercontent.com%2Fmamchyts%2Fbenchmark-thumbnails%2Fmaster%2Fnature-wallpaper-1920x1080.jpg
    1280x720
        ./wrk -t1 -c1 -d60s http://localhost:8081/unsafe/1280x720/https%3A%2F%2Fraw.githubusercontent.com%2Fmamchyts%2Fbenchmark-thumbnails%2Fmaster%2Fnature-wallpaper-1920x1080.jpg

thumbor-cache:
    320x240
        ./wrk -t1 -c1 -d60s http://localhost:8082/unsafe/320x240/https%3A%2F%2Fraw.githubusercontent.com%2Fmamchyts%2Fbenchmark-thumbnails%2Fmaster%2Fnature-wallpaper-1920x1080.jpg
    854x480
        ./wrk -t1 -c1 -d60s http://localhost:8082/unsafe/854x480/https%3A%2F%2Fraw.githubusercontent.com%2Fmamchyts%2Fbenchmark-thumbnails%2Fmaster%2Fnature-wallpaper-1920x1080.jpg
    1280x720
        ./wrk -t1 -c1 -d60s http://localhost:8082/unsafe/1280x720/https%3A%2F%2Fraw.githubusercontent.com%2Fmamchyts%2Fbenchmark-thumbnails%2Fmaster%2Fnature-wallpaper-1920x1080.jpg

imaginary:
    320x240
        ./wrk -t1 -c1 -d60s 'http://localhost:8083/enlarge?width=320&height=240&url=https%3A%2F%2Fraw.githubusercontent.com%2Fmamchyts%2Fbenchmark-thumbnails%2Fmaster%2Fnature-wallpaper-1920x1080.jpg'
    854x480
        ./wrk -t1 -c1 -d60s 'http://localhost:8083/enlarge?width=854&height=480&url=https%3A%2F%2Fraw.githubusercontent.com%2Fmamchyts%2Fbenchmark-thumbnails%2Fmaster%2Fnature-wallpaper-1920x1080.jpg'
    1280x720
        ./wrk -t1 -c1 -d60s 'http://localhost:8083/enlarge?width=1280&height=720&url=https%3A%2F%2Fraw.githubusercontent.com%2Fmamchyts%2Fbenchmark-thumbnails%2Fmaster%2Fnature-wallpaper-1920x1080.jpg'

picfit:
    320x240
        ./wrk -t1 -c1 -d60s 'http://localhost:8084/display?w=320&h=240&op=thumbnail&url=https%3A%2F%2Fraw.githubusercontent.com%2Fmamchyts%2Fbenchmark-thumbnails%2Fmaster%2Fnature-wallpaper-1920x1080.jpg'
    854x480
        ./wrk -t1 -c1 -d60s 'http://localhost:8084/display?w=854&h=480&op=thumbnail&url=https%3A%2F%2Fraw.githubusercontent.com%2Fmamchyts%2Fbenchmark-thumbnails%2Fmaster%2Fnature-wallpaper-1920x1080.jpg'
    1280x720
        ./wrk -t1 -c1 -d60s 'http://localhost:8084/display?w=1280&h=720&op=thumbnail&url=https%3A%2F%2Fraw.githubusercontent.com%2Fmamchyts%2Fbenchmark-thumbnails%2Fmaster%2Fnature-wallpaper-1920x1080.jpg'

picfit-cache:
    320x240
        ./wrk -t1 -c1 -d60s 'http://localhost:8085/display?w=320&h=240&op=thumbnail&url=https%3A%2F%2Fraw.githubusercontent.com%2Fmamchyts%2Fbenchmark-thumbnails%2Fmaster%2Fnature-wallpaper-1920x1080.jpg'
    854x480
        ./wrk -t1 -c1 -d60s 'http://localhost:8085/display?w=854&h=480&op=thumbnail&url=https%3A%2F%2Fraw.githubusercontent.com%2Fmamchyts%2Fbenchmark-thumbnails%2Fmaster%2Fnature-wallpaper-1920x1080.jpg'
    1280x720
        ./wrk -t1 -c1 -d60s 'http://localhost:8085/display?w=1280&h=720&op=thumbnail&url=https%3A%2F%2Fraw.githubusercontent.com%2Fmamchyts%2Fbenchmark-thumbnails%2Fmaster%2Fnature-wallpaper-1920x1080.jpg'

imageproxy:
    320x240
        ./wrk -t1 -c1 -d60s http://localhost:8086/320x240/https://raw.githubusercontent.com/mamchyts/benchmark-thumbnails/master/nature-wallpaper-1920x1080.jpg
    854x480
        ./wrk -t1 -c1 -d60s http://localhost:8086/854x480/https://raw.githubusercontent.com/mamchyts/benchmark-thumbnails/master/nature-wallpaper-1920x1080.jpg
    1280x720
        ./wrk -t1 -c1 -d60s http://localhost:8086/1280x720/https://raw.githubusercontent.com/mamchyts/benchmark-thumbnails/master/nature-wallpaper-1920x1080.jpg

imageproxy-cache:
    320x240
        ./wrk -t1 -c1 -d60s http://localhost:8087/320x240/https://raw.githubusercontent.com/mamchyts/benchmark-thumbnails/master/nature-wallpaper-1920x1080.jpg
    854x480
        ./wrk -t1 -c1 -d60s http://localhost:8087/854x480/https://raw.githubusercontent.com/mamchyts/benchmark-thumbnails/master/nature-wallpaper-1920x1080.jpg
    1280x720
        ./wrk -t1 -c1 -d60s http://localhost:8087/1280x720/https://raw.githubusercontent.com/mamchyts/benchmark-thumbnails/master/nature-wallpaper-1920x1080.jpg
```