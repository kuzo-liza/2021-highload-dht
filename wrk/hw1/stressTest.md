# PUT
### wrk2 
#### option 1
Обстрел производился одним потоком с одним соединением. Заданную нагрузку сервер отрабатывает успешно - 1999.99 запросов в секунду. Среднеквадратичное отклонение составляет 96.87%. За 10 минут было обработано успешно почти 1.2 млн запросов. Распределение Latency неравномерно - при 99.000% время ответа резко возрастает, однако далее держится на том же уровне. Это объясняется тем, что запись производится сначала в MemTable, а при ее заполнении происходит flash на диск, что вызывает скачок времени ответа.
    
    Running 10m test @ http://localhost:8080
    1 threads and 1 connections
    Thread calibration: mean lat.: 1.293ms, rate sampling interval: 10ms
    Thread Stats   Avg      Stdev     Max   +/- Stdev
    Latency    44.81ms  262.60ms   2.73s    96.87%
    Req/Sec     2.12k     1.28k   28.00k    96.23%
    Latency Distribution (HdrHistogram - Recorded Latency)
    50.000%    1.29ms
    75.000%    1.80ms
    90.000%    2.28ms
    99.000%    1.73s
    99.900%    2.50s
    99.990%    2.70s
    99.999%    2.73s
    100.000%    2.74s

    Detailed Percentile spectrum:
    Value   Percentile   TotalCount 1/(1-Percentile)

       0.046     0.000000            1         1.00
       0.428     0.100000       118190         1.11
       0.697     0.200000       236194         1.25
       0.944     0.300000       354031         1.43
       1.146     0.400000       472204         1.67
       1.294     0.500000       590144         2.00
       1.367     0.550000       649290         2.22
       1.440     0.600000       708003         2.50
       1.530     0.650000       767071         2.86
       1.658     0.700000       826070         3.33
       1.803     0.750000       885284         4.00
       1.879     0.775000       914678         4.44
       1.955     0.800000       944000         5.00
       2.032     0.825000       973655         5.71
       2.111     0.850000      1003306         6.67
       2.191     0.875000      1032791         8.00
       2.233     0.887500      1047438         8.89
       2.279     0.900000      1062334        10.00
       2.327     0.912500      1077017        11.43
       2.379     0.925000      1091981        13.33
       2.437     0.937500      1106671        16.00
       2.477     0.943750      1113731        17.78
       2.553     0.950000      1121026        20.00
       3.095     0.956250      1128375        22.86
      17.279     0.962500      1135738        26.67
     308.223     0.968750      1143116        32.00
     517.887     0.971875      1146800        35.56
     727.039     0.975000      1150489        40.00
     936.959     0.978125      1154178        45.71
    1146.879     0.981250      1157872        53.33
    1354.751     0.984375      1161556        64.00
    1459.199     0.985938      1163407        71.11
    1562.623     0.987500      1165254        80.00
    1667.071     0.989062      1167081        91.43
    1772.543     0.990625      1168936       106.67
    1876.991     0.992188      1170775       128.00
    1929.215     0.992969      1171691       142.22
    1982.463     0.993750      1172626       160.00
    2033.663     0.994531      1173534       182.86
    2089.983     0.995313      1174459       213.33
    2150.399     0.996094      1175403       256.00
    2179.071     0.996484      1175853       284.44
    2213.887     0.996875      1176323       320.00
    2254.847     0.997266      1176770       365.71
    2306.047     0.997656      1177223       426.67
    2359.295     0.998047      1177693       512.00
    2385.919     0.998242      1177930       568.89
    2410.495     0.998437      1178157       640.00
    2441.215     0.998633      1178382       731.43
    2476.031     0.998828      1178617       853.33
    2508.799     0.999023      1178841      1024.00
    2525.183     0.999121      1178952      1137.78
    2543.615     0.999219      1179077      1280.00
    2559.999     0.999316      1179187      1462.86
    2582.527     0.999414      1179301      1706.67
    2607.103     0.999512      1179417      2048.00
    2619.391     0.999561      1179473      2275.56
    2631.679     0.999609      1179529      2560.00
    2643.967     0.999658      1179584      2925.71
    2656.255     0.999707      1179642      3413.33
    2668.543     0.999756      1179701      4096.00
    2674.687     0.999780      1179730      4551.11
    2680.831     0.999805      1179762      5120.00
    2686.975     0.999829      1179792      5851.43
    2693.119     0.999854      1179822      6826.67
    2699.263     0.999878      1179853      8192.00
    2701.311     0.999890      1179863      9102.22
    2703.359     0.999902      1179872     10240.00
    2707.455     0.999915      1179893     11702.86
    2709.503     0.999927      1179902     13653.33
    2713.599     0.999939      1179923     16384.00
    2713.599     0.999945      1179923     18204.44
    2715.647     0.999951      1179933     20480.00
    2717.695     0.999957      1179942     23405.71
    2719.743     0.999963      1179946     27306.67
    2721.791     0.999969      1179952     32768.00
    2723.839     0.999973      1179957     36408.89
    2725.887     0.999976      1179962     40960.00
    2725.887     0.999979      1179962     46811.43
    2727.935     0.999982      1179969     54613.33
    2727.935     0.999985      1179969     65536.00
    2729.983     0.999986      1179975     72817.78
    2729.983     0.999988      1179975     81920.00
    2729.983     0.999989      1179975     93622.86
    2732.031     0.999991      1179980    109226.67
    2732.031     0.999992      1179980    131072.00
    2732.031     0.999993      1179980    145635.56
    2732.031     0.999994      1179980    163840.00
    2734.079     0.999995      1179985    187245.71
    2734.079     0.999995      1179985    218453.33
    2734.079     0.999996      1179985    262144.00
    2734.079     0.999997      1179985    291271.11
    2734.079     0.999997      1179985    327680.00
    2734.079     0.999997      1179985    374491.43
    2734.079     0.999998      1179985    436906.67
    2734.079     0.999998      1179985    524288.00
    2734.079     0.999998      1179985    582542.22
    2736.127     0.999998      1179987    655360.00
    2736.127     1.000000      1179987          inf
    #[Mean    =       44.805, StdDeviation   =      262.595]
    #[Max     =     2734.080, Total count    =      1179987]
    #[Buckets =           27, SubBuckets     =         2048]
    ----------------------------------------------------------
    1199996 requests in 10.00m, 76.68MB read
    Socket errors: connect 0, read 0, write 0, timeout 4
    Requests/sec:   1999.99
    Transfer/sec:    130.86KB

#### option 2
Обстрел производился одним потоком с одним соединением. Заданную нагрузку сервер отрабатывает успешно - 999.99 запросов в секунду. Среднеквадратичное отклонение составляет 99.12%. За 2 минуты было обработано успешно почти 120 тысяч запросов. Распределение Latency выглядит более равномерным, чем в первом случае, однако также присутствует скачок при начале записи данных на диск - при 99.900% время ответа возрастает.

    Running 2m test @ http://localhost:8080
    1 threads and 1 connections
    Thread calibration: mean lat.: 1.655ms, rate sampling interval: 10ms
    Thread Stats   Avg      Stdev     Max   +/- Stdev
    Latency     1.44ms    2.46ms  79.23ms   99.12%
    Req/Sec     1.06k   146.94     5.09k    77.11%
    Latency Distribution (HdrHistogram - Recorded Latency)
    50.000%    1.27ms
    75.000%    1.64ms
    90.000%    2.03ms
    99.000%    2.76ms
    99.900%   44.70ms
    99.990%   74.30ms
    99.999%   78.65ms
    100.000%   79.29ms

    Detailed Percentile spectrum:
    Value   Percentile   TotalCount 1/(1-Percentile)

       0.089     0.000000            1         1.00
       0.522     0.100000        11010         1.11
       0.781     0.200000        22038         1.25
       0.994     0.300000        33030         1.43
       1.135     0.400000        44026         1.67
       1.268     0.500000        55086         2.00
       1.335     0.550000        60560         2.22
       1.405     0.600000        66067         2.50
       1.480     0.650000        71540         2.86
       1.560     0.700000        77012         3.33
       1.643     0.750000        82531         4.00
       1.696     0.775000        85282         4.44
       1.761     0.800000        88013         5.00
       1.827     0.825000        90758         5.71
       1.893     0.850000        93520         6.67
       1.961     0.875000        96268         8.00
       1.996     0.887500        97645         8.89
       2.034     0.900000        99019        10.00
       2.071     0.912500       100384        11.43
       2.111     0.925000       101763        13.33
       2.157     0.937500       103131        16.00
       2.183     0.943750       103824        17.78
       2.209     0.950000       104532        20.00
       2.233     0.956250       105216        22.86
       2.259     0.962500       105887        26.67
       2.285     0.968750       106596        32.00
       2.297     0.971875       106947        35.56
       2.311     0.975000       107293        40.00
       2.323     0.978125       107602        45.71
       2.339     0.981250       107951        53.33
       2.361     0.984375       108281        64.00
       2.381     0.985938       108453        71.11
       2.413     0.987500       108625        80.00
       2.501     0.989062       108792        91.43
       3.163     0.990625       108963       106.67
       5.607     0.992188       109136       128.00
       6.999     0.992969       109221       142.22
       9.207     0.993750       109307       160.00
      11.807     0.994531       109394       182.86
      14.743     0.995313       109479       213.33
      17.903     0.996094       109565       256.00
      19.343     0.996484       109609       284.44
      20.623     0.996875       109652       320.00
      23.151     0.997266       109694       365.71
      25.583     0.997656       109737       426.67
      29.439     0.998047       109780       512.00
      31.487     0.998242       109801       568.89
      34.303     0.998437       109823       640.00
      38.399     0.998633       109844       731.43
      41.951     0.998828       109866       853.33
      45.375     0.999023       109887      1024.00
      46.591     0.999121       109898      1137.78
      48.031     0.999219       109909      1280.00
      49.727     0.999316       109919      1462.86
      51.167     0.999414       109930      1706.67
      52.575     0.999512       109941      2048.00
      54.271     0.999561       109946      2275.56
      58.911     0.999609       109952      2560.00
      62.911     0.999658       109957      2925.71
      64.223     0.999707       109962      3413.33
      67.391     0.999756       109968      4096.00
      68.735     0.999780       109970      4551.11
      69.887     0.999805       109973      5120.00
      71.359     0.999829       109977      5851.43
      71.935     0.999854       109978      6826.67
      73.791     0.999878       109981      8192.00
      74.175     0.999890       109982      9102.22
      75.135     0.999902       109984     10240.00
      75.839     0.999915       109985     11702.86
      76.287     0.999927       109986     13653.33
      77.055     0.999939       109988     16384.00
      77.055     0.999945       109988     18204.44
      77.439     0.999951       109989     20480.00
      77.823     0.999957       109990     23405.71
      77.823     0.999963       109990     27306.67
      78.143     0.999969       109992     32768.00
      78.143     0.999973       109992     36408.89
      78.143     0.999976       109992     40960.00
      78.143     0.999979       109992     46811.43
      78.143     0.999982       109992     54613.33
      78.655     0.999985       109993     65536.00
      78.655     0.999986       109993     72817.78
      78.655     0.999988       109993     81920.00
      78.655     0.999989       109993     93622.86
      78.655     0.999991       109993    109226.67
      79.295     0.999992       109994    131072.00
      79.295     1.000000       109994          inf
    #[Mean    =        1.439, StdDeviation   =        2.459]
    #[Max     =       79.232, Total count    =       109994]
    #[Buckets =           27, SubBuckets     =         2048]
    ----------------------------------------------------------
    119999 requests in 2.00m, 7.67MB read
    Requests/sec:    999.99
    Transfer/sec:     65.43KB

### Profiler
Добавлен конфиг для логирования, чтобы ресурсы не тратились на это. 

Было увеличено время обстрела до 10 минут. На графиках видно, что происходит flush данных на диск.

9.35% тратится на запись данных на диск, 4.07% - на запись в MemTable, таким образом на работу с DAO уходит 13.47%.
Мониторинг доступных каналов занимает 30% ресурсов CPU. Обработка запросов занимает 48%, запись в сокет - 28%, чтение из сокета - 15%. Процесс "прогрет", поэтому JIT компилятор тратит всего 3% ресурсов.

[cpu flameGraph](put_cpu.html)

6.65% памяти занимает flush данных на диск, добавление в MemTable 3.4%, на работу с DAO уходит 13% памяти. Обработка запросов занимает 56%, парсинг запроса - 14.42%. Заметно, что ресурсы тратятся на дублирование байт буферов.

[alloc flameGraph](put_alloc.html)

# GET

### wrk2
#### option 1
Обстрел производился одним потоком с одним соединением. Заданную нагрузку сервер отрабатывает успешно - 999.99 запросов в секунду. Среднеквадратичное отклонение составляет 94.96%. За 2 минуты было обработано успешно около 120 тысяч запросов. Распределение Latency более равномерно, чем в PUT - при 99.000% время ответа немного возрастает из-за того, что происходит поиск данных в таблицах на диске.

    Running 2m test @ http://localhost:8080
    1 threads and 1 connections
    Thread calibration: mean lat.: 71.518ms, rate sampling interval: 786ms
    Thread Stats   Avg      Stdev     Max   +/- Stdev
    Latency     1.41ms    1.09ms  40.67ms   94.96%
    Req/Sec     1.00k     1.87     1.01k    95.68%
    Latency Distribution (HdrHistogram - Recorded Latency)
    50.000%    1.34ms
    75.000%    1.74ms
    90.000%    2.13ms
    99.000%    3.24ms
    99.900%   16.17ms
    99.990%   38.65ms
    99.999%   40.54ms
    100.000%   40.70ms

    Detailed Percentile spectrum:
    Value   Percentile   TotalCount 1/(1-Percentile)

       0.086     0.000000            1         1.00
       0.602     0.100000        11022         1.11
       0.842     0.200000        22038         1.25
       1.041     0.300000        33010         1.43
       1.197     0.400000        43998         1.67
       1.340     0.500000        55029         2.00
       1.414     0.550000        60536         2.22
       1.490     0.600000        66028         2.50
       1.571     0.650000        71553         2.86
       1.655     0.700000        77012         3.33
       1.741     0.750000        82507         4.00
       1.790     0.775000        85296         4.44
       1.844     0.800000        88019         5.00
       1.902     0.825000        90773         5.71
       1.964     0.850000        93508         6.67
       2.036     0.875000        96272         8.00
       2.079     0.887500        97622         8.89
       2.129     0.900000        99011        10.00
       2.187     0.912500       100391        11.43
       2.247     0.925000       101769        13.33
       2.309     0.937500       103124        16.00
       2.341     0.943750       103817        17.78
       2.375     0.950000       104501        20.00
       2.415     0.956250       105206        22.86
       2.455     0.962500       105895        26.67
       2.495     0.968750       106580        32.00
       2.517     0.971875       106917        35.56
       2.541     0.975000       107254        40.00
       2.575     0.978125       107597        45.71
       2.623     0.981250       107933        53.33
       2.741     0.984375       108282        64.00
       2.817     0.985938       108448        71.11
       2.943     0.987500       108620        80.00
       3.101     0.989062       108794        91.43
       3.353     0.990625       108963       106.67
       3.675     0.992188       109135       128.00
       3.849     0.992969       109221       142.22
       4.103     0.993750       109307       160.00
       4.375     0.994531       109393       182.86
       4.787     0.995313       109479       213.33
       5.327     0.996094       109566       256.00
       5.643     0.996484       109608       284.44
       6.219     0.996875       109651       320.00
       6.727     0.997266       109695       365.71
       7.563     0.997656       109737       426.67
       9.207     0.998047       109780       512.00
      10.343     0.998242       109801       568.89
      11.855     0.998437       109823       640.00
      13.791     0.998633       109844       731.43
      15.111     0.998828       109866       853.33
      16.367     0.999023       109887      1024.00
      17.631     0.999121       109898      1137.78
      18.703     0.999219       109909      1280.00
      19.455     0.999316       109919      1462.86
      20.527     0.999414       109930      1706.67
      24.127     0.999512       109941      2048.00
      25.695     0.999561       109946      2275.56
      26.847     0.999609       109952      2560.00
      28.335     0.999658       109957      2925.71
      29.999     0.999707       109962      3413.33
      30.911     0.999756       109968      4096.00
      31.999     0.999780       109970      4551.11
      34.015     0.999805       109973      5120.00
      35.551     0.999829       109976      5851.43
      37.023     0.999854       109978      6826.67
      37.983     0.999878       109981      8192.00
      38.335     0.999890       109982      9102.22
      38.687     0.999902       109984     10240.00
      39.327     0.999915       109985     11702.86
      39.359     0.999927       109986     13653.33
      39.999     0.999939       109990     16384.00
      39.999     0.999945       109990     18204.44
      39.999     0.999951       109990     20480.00
      39.999     0.999957       109990     23405.71
      39.999     0.999963       109990     27306.67
      40.287     0.999969       109991     32768.00
      40.287     0.999973       109991     36408.89
      40.319     0.999976       109992     40960.00
      40.319     0.999979       109992     46811.43
      40.319     0.999982       109992     54613.33
      40.543     0.999985       109993     65536.00
      40.543     0.999986       109993     72817.78
      40.543     0.999988       109993     81920.00
      40.543     0.999989       109993     93622.86
      40.543     0.999991       109993    109226.67
      40.703     0.999992       109994    131072.00
      40.703     1.000000       109994          inf
    #[Mean    =        1.409, StdDeviation   =        1.087]
    #[Max     =       40.672, Total count    =       109994]
    #[Buckets =           27, SubBuckets     =         2048]
    ----------------------------------------------------------
    119999 requests in 2.00m, 8.35MB read
    Requests/sec:    999.99
    Transfer/sec:     71.28KB

#### option 2
Обстрел производился одним потоком с одним соединением. Заданную нагрузку сервер отрабатывает успешно - 1999.98 запросов в секунду. Среднеквадратичное отклонение составляет 97.67%. За 3 минуты было обработано успешно более 360 тысяч запросов. Распределение Latency чуть менее равномерно, чем в первом случае - при 99.900% время ответа возрастает потому, что происходит поиск данных в таблицах на диске.

    Running 3m test @ http://localhost:8080
    1 threads and 1 connections
    Thread calibration: mean lat.: 4.400ms, rate sampling interval: 10ms
    Thread Stats   Avg      Stdev     Max   +/- Stdev
    Latency     1.93ms    5.20ms 145.28ms   97.67%
    Req/Sec     2.11k   324.75     5.80k    82.64%
    Latency Distribution (HdrHistogram - Recorded Latency)
    50.000%    1.29ms
    75.000%    1.80ms
    90.000%    2.58ms
    99.000%   16.21ms
    99.900%   90.75ms
    99.990%  141.05ms
    99.999%  145.02ms
    100.000%  145.41ms

    Detailed Percentile spectrum:
    Value   Percentile   TotalCount 1/(1-Percentile)

       0.081     0.000000            1         1.00
       0.469     0.100000        34070         1.11
       0.711     0.200000        68021         1.25
       0.928     0.300000       102148         1.43
       1.120     0.400000       136038         1.67
       1.291     0.500000       170128         2.00
       1.371     0.550000       187119         2.22
       1.454     0.600000       204085         2.50
       1.544     0.650000       221152         2.86
       1.653     0.700000       238110         3.33
       1.801     0.750000       255075         4.00
       1.893     0.775000       263565         4.44
       1.993     0.800000       272057         5.00
       2.105     0.825000       280617         5.71
       2.229     0.850000       289107         6.67
       2.375     0.875000       297505         8.00
       2.467     0.887500       301806         8.89
       2.577     0.900000       305996        10.00
       2.733     0.912500       310275        11.43
       2.975     0.925000       314508        13.33
       3.323     0.937500       318754        16.00
       3.557     0.943750       320870        17.78
       3.859     0.950000       322991        20.00
       4.263     0.956250       325116        22.86
       4.835     0.962500       327247        26.67
       5.583     0.968750       329364        32.00
       6.095     0.971875       330426        35.56
       6.723     0.975000       331487        40.00
       7.511     0.978125       332553        45.71
       8.567     0.981250       333614        53.33
      10.303     0.984375       334677        64.00
      11.599     0.985938       335208        71.11
      12.983     0.987500       335739        80.00
      14.599     0.989062       336269        91.43
      17.359     0.990625       336799       106.67
      20.863     0.992188       337334       128.00
      22.479     0.992969       337598       142.22
      24.175     0.993750       337862       160.00
      25.903     0.994531       338128       182.86
      28.607     0.995313       338393       213.33
      32.127     0.996094       338658       256.00
      33.791     0.996484       338792       284.44
      35.359     0.996875       338924       320.00
      38.655     0.997266       339059       365.71
      45.247     0.997656       339190       426.67
      53.951     0.998047       339322       512.00
      70.079     0.998242       339390       568.89
      76.991     0.998437       339455       640.00
      83.391     0.998633       339522       731.43
      86.655     0.998828       339589       853.33
      91.391     0.999023       339654      1024.00
      93.503     0.999121       339692      1137.78
      95.679     0.999219       339721      1280.00
     103.615     0.999316       339754      1462.86
     111.935     0.999414       339787      1706.67
     119.423     0.999512       339820      2048.00
     123.583     0.999561       339837      2275.56
     126.207     0.999609       339854      2560.00
     130.239     0.999658       339870      2925.71
     134.143     0.999707       339887      3413.33
     138.367     0.999756       339903      4096.00
     139.007     0.999780       339912      4551.11
     139.391     0.999805       339921      5120.00
     139.647     0.999829       339928      5851.43
     140.031     0.999854       339937      6826.67
     140.415     0.999878       339945      8192.00
     140.799     0.999890       339949      9102.22
     141.311     0.999902       339954     10240.00
     141.951     0.999915       339958     11702.86
     142.719     0.999927       339962     13653.33
     143.359     0.999939       339966     16384.00
     143.487     0.999945       339968     18204.44
     143.743     0.999951       339970     20480.00
     143.871     0.999957       339972     23405.71
     143.999     0.999963       339976     27306.67
     143.999     0.999969       339976     32768.00
     144.127     0.999973       339977     36408.89
     144.255     0.999976       339978     40960.00
     144.383     0.999979       339979     46811.43
     144.511     0.999982       339980     54613.33
     144.767     0.999985       339981     65536.00
     144.895     0.999986       339982     72817.78
     144.895     0.999988       339982     81920.00
     145.023     0.999989       339983     93622.86
     145.023     0.999991       339983    109226.67
     145.151     0.999992       339985    131072.00
     145.151     0.999993       339985    145635.56
     145.151     0.999994       339985    163840.00
     145.151     0.999995       339985    187245.71
     145.151     0.999995       339985    218453.33
     145.151     0.999996       339985    262144.00
     145.151     0.999997       339985    291271.11
     145.151     0.999997       339985    327680.00
     145.407     0.999997       339986    374491.43
     145.407     1.000000       339986          inf
    #[Mean    =        1.928, StdDeviation   =        5.200]
    #[Max     =      145.280, Total count    =       339986]
    #[Buckets =           27, SubBuckets     =         2048]
    ----------------------------------------------------------
    359996 requests in 3.00m, 25.29MB read
    Requests/sec:   1999.98
    Transfer/sec:    143.87KB

### Profiler
Добавлен конфиг для логирования, чтобы ресурсы не тратились на это.

Обстрел выполнялся по заполненной ранее базе. 49% ресурсов CPU уходит на работу с DAO, а также 9% занимает итерирование по записям. Запись в сокет занимает 12%, мониторинг каналов - 11%, чтение из сокета 7%. Обработка запросов занимает 74%. Процесс "прогрет", поэтому JIT компилятор тратит 5% ресурсов.

[cpu flameGraph](get_cpu.html)

83% памяти занимает работа с DAO. На обработку запросов уходит 92%, на парсинг запроса - 3.55%. Так же как и в PUT, ресурсы тратятся на дублирование байт буферов.

[alloc flameGraph](get_alloc.html)

## Выводы

Много времени уходит на чтение и запись в сокеты, стоит подумать над использованием другого протокола для работы с сетью.
Также в методе flush записываются отдельно ключ и значение, можно попробовать буферизировать ключ и значение вместе и записывать их вместе, чтобы системный вызов write был вызван 1 раз. 
Кроме того, можно посмотреть, кто генерирует мусор и уменьшить работу сборщика мусора.
