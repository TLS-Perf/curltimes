# curltimes.sh

curl measurement tool for HTTPS connection times using shell script modified from https://nooshu.github.io/blog/2020/07/30/measuring-tls-13-ipv4-ipv6-performance/

# Usage

```
./curltimes.sh 
Usage:

TLS 1.2 max tests
./curltimes.sh json https://domain.com
./curltimes.sh csv https://domain.com

TLS 1.3 max tests
./curltimes.sh json-max https://domain.com
./curltimes.sh csv-max https://domain.com

CSV Summary
./curltimes.sh csv-sum https://domain.com
./curltimes.sh csv-max-sum https://domain.com
```

# Examples

json output with TLS 1.2 max

```
./curltimes.sh json https://servermanager.guide
["DNS","Connect","SSL","Wait","TTFB","Total Time"]
{
        "time_dns":             0.002564,
        "time_connect":         0.011402,
        "time_appconnect":      0.038828,
        "time_pretransfer":     0.038916,
        "time_ttfb":            0.095125,
        "time_total":           0.103974
}{
        "time_dns":             0.002488,
        "time_connect":         0.011142,
        "time_appconnect":      0.034979,
        "time_pretransfer":     0.035068,
        "time_ttfb":            0.071230,
        "time_total":           0.080085
}{
        "time_dns":             0.002347,
        "time_connect":         0.011030,
        "time_appconnect":      0.038583,
        "time_pretransfer":     0.038665,
        "time_ttfb":            0.081110,
        "time_total":           0.090616
}
```

json output with TLS 1.3 max

```
./curltimes.sh json-max https://servermanager.guide
["DNS","Connect","SSL","Wait","TTFB","Total Time"]
{
        "time_dns":             0.002475,
        "time_connect":         0.011114,
        "time_appconnect":      0.032894,
        "time_pretransfer":     0.032987,
        "time_ttfb":            0.070362,
        "time_total":           0.078909
}{
        "time_dns":             0.016671,
        "time_connect":         0.025292,
        "time_appconnect":      0.041496,
        "time_pretransfer":     0.041585,
        "time_ttfb":            0.078091,
        "time_total":           0.084820
}{
        "time_dns":             0.002357,
        "time_connect":         0.011059,
        "time_appconnect":      0.027810,
        "time_pretransfer":     0.027896,
        "time_ttfb":            0.070568,
        "time_total":           0.079413
}
```

csv output with TLS 1.2 max

```
./curltimes.sh csv https://servermanager.guide        
["DNS","Connect","SSL","Wait","TTFB","Total Time"]
0.002499,0.011232,0.038939,0.039032,0.070107,0.078926
0.002468,0.011151,0.045335,0.04542,0.093941,0.102807
0.002477,0.011191,0.037536,0.037619,0.065233,0.075599
```

csv output with TLS 1.3 max

```
./curltimes.sh csv-max https://servermanager.guide
["DNS","Connect","SSL","Wait","TTFB","Total Time"]
0.014534,0.023231,0.03993,0.040021,0.069676,0.078247
0.00241,0.011095,0.027924,0.028012,0.061294,0.069808
0.002393,0.011048,0.02692,0.027,0.055102,0.064368
```

# process metrics

Using datamash to provide summary metrics for all recorded data points

csv-sum output with TLS 1.2 max

```
./curltimes.sh csv-sum https://servermanager.guide
0.002435,0.011094,0.045748,0.045843,0.082256,0.090951
0.002436,0.011077,0.035719,0.035805,0.06275,0.071497
0.002501,0.011161,0.037638,0.037724,0.071217,0.080031

time_dns 
  avg: 0.002457 
  min: 0.002435 
  max: 0.002501 
  75%: 0.002468 
  95%: 0.002495 
  99%: 0.002500
time_connect 
  avg: 0.011111 
  min: 0.011077 
  max: 0.011161 
  75%: 0.011128 
  95%: 0.011154 
  99%: 0.011160
time_appconnect 
  avg: 0.039702 
  min: 0.035719 
  max: 0.045748 
  75%: 0.041693 
  95%: 0.044937 
  99%: 0.045586
time_pretransfer 
  avg: 0.039791 
  min: 0.035805 
  max: 0.045843 
  75%: 0.041783 
  95%: 0.045031 
  99%: 0.045681
time_ttfb 
  avg: 0.072074 
  min: 0.062750 
  max: 0.082256 
  75%: 0.076737 
  95%: 0.081152 
  99%: 0.082035
time_total 
  avg: 0.080826 
  min: 0.071497 
  max: 0.090951 
  75%: 0.085491 
  95%: 0.089859 
  99%: 0.090733

time_dns
avg:,min:,max:,75%:,95%:,99%:
0.002457,0.002435,0.002501,0.002468,0.002495,0.002500
time_connect
avg:,min:,max:,75%:,95%:,99%:
0.011111,0.011077,0.011161,0.011128,0.011154,0.011160
time_appconnect
avg:,min:,max:,75%:,95%:,99%:
0.039702,0.035719,0.045748,0.041693,0.044937,0.045586
time_pretransfer
avg:,min:,max:,75%:,95%:,99%:
0.039791,0.035805,0.045843,0.041783,0.045031,0.045681
time_ttfb
avg:,min:,max:,75%:,95%:,99%:
0.072074,0.062750,0.082256,0.076737,0.081152,0.082035
time_total
avg:,min:,max:,75%:,95%:,99%:
0.080826,0.071497,0.090951,0.085491,0.089859,0.090733
```

csv-max-sum output with TLS 1.3 max

```
./curltimes.sh csv-max-sum https://servermanager.guide
0.002516,0.011186,0.02821,0.028291,0.056036,0.064954
0.002426,0.011152,0.027389,0.027468,0.050343,0.058981
0.002459,0.011125,0.030485,0.030565,0.068301,0.0769

time_dns 
  avg: 0.002467 
  min: 0.002426 
  max: 0.002516 
  75%: 0.002487 
  95%: 0.002510 
  99%: 0.002515
time_connect 
  avg: 0.011154 
  min: 0.011125 
  max: 0.011186 
  75%: 0.011169 
  95%: 0.011183 
  99%: 0.011185
time_appconnect 
  avg: 0.028695 
  min: 0.027389 
  max: 0.030485 
  75%: 0.029348 
  95%: 0.030258 
  99%: 0.030439
time_pretransfer 
  avg: 0.028775 
  min: 0.027468 
  max: 0.030565 
  75%: 0.029428 
  95%: 0.030338 
  99%: 0.030520
time_ttfb 
  avg: 0.058227 
  min: 0.050343 
  max: 0.068301 
  75%: 0.062168 
  95%: 0.067075 
  99%: 0.068056
time_total 
  avg: 0.066945 
  min: 0.058981 
  max: 0.076900 
  75%: 0.070927 
  95%: 0.075705 
  99%: 0.076661

time_dns
avg:,min:,max:,75%:,95%:,99%:
0.002467,0.002426,0.002516,0.002487,0.002510,0.002515
time_connect
avg:,min:,max:,75%:,95%:,99%:
0.011154,0.011125,0.011186,0.011169,0.011183,0.011185
time_appconnect
avg:,min:,max:,75%:,95%:,99%:
0.028695,0.027389,0.030485,0.029348,0.030258,0.030439
time_pretransfer
avg:,min:,max:,75%:,95%:,99%:
0.028775,0.027468,0.030565,0.029428,0.030338,0.030520
time_ttfb
avg:,min:,max:,75%:,95%:,99%:
0.058227,0.050343,0.068301,0.062168,0.067075,0.068056
time_total
avg:,min:,max:,75%:,95%:,99%:
0.066945,0.058981,0.076900,0.070927,0.075705,0.076661
```

TLS 1.2 vs TLS 1.3 for 11 run diff compare

```
diff -u <(./curltimes.sh csv-sum https://servermanager.guide) <(./curltimes.sh csv-max-sum https://servermanager.guide)
--- /dev/fd/63  2020-08-01 13:18:21.626452903 +0000
+++ /dev/fd/62  2020-08-01 13:18:21.626452903 +0000
@@ -1,73 +1,73 @@
-0.002436,0.011037,0.034963,0.03504,0.067372,0.076111
-0.002399,0.011062,0.038936,0.03901,0.058978,0.067808
-0.002315,0.010938,0.040412,0.040486,0.074658,0.083294
-0.002391,0.011042,0.035051,0.035133,0.05906,0.067943
-0.002457,0.011058,0.049771,0.049847,0.077074,0.085864
-0.002544,0.011218,0.040902,0.040992,0.075093,0.083711
-0.002392,0.011048,0.035923,0.036011,0.062979,0.071847
-0.002378,0.011077,0.039314,0.039388,0.069771,0.078883
-0.002488,0.011108,0.038195,0.038276,0.07313,0.082034
-0.002404,0.011052,0.039762,0.039844,0.07213,0.081367
-0.002412,0.011062,0.035379,0.035465,0.061553,0.070373
+0.002853,0.011497,0.026521,0.026608,0.06211,0.07094
+0.00244,0.011088,0.026456,0.026542,0.051307,0.059805
+0.002583,0.011226,0.027035,0.027121,0.049788,0.058538
+0.002477,0.011097,0.026352,0.026431,0.051805,0.060649
+0.002429,0.011041,0.026421,0.026499,0.051938,0.060378
+0.002098,0.010756,0.028408,0.028484,0.069526,0.078088
+0.002434,0.011133,0.026804,0.026886,0.050501,0.05989
+0.002096,0.010772,0.027185,0.027273,0.053989,0.062698
+0.002402,0.011059,0.026852,0.026928,0.047318,0.056316
+0.002553,0.011231,0.030412,0.030487,0.064271,0.07322
+0.002067,0.010753,0.028232,0.028307,0.059697,0.06847
 
 time_dns 
-  avg: 0.002420 
-  min: 0.002315 
-  max: 0.002544 
-  75%: 0.002446 
-  95%: 0.002516 
-  99%: 0.002538
+  avg: 0.002403 
+  min: 0.002067 
+  max: 0.002853 
+  75%: 0.002515 
+  95%: 0.002718 
+  99%: 0.002826
 time_connect 
-  avg: 0.011064 
-  min: 0.010938 
-  max: 0.011218 
-  75%: 0.011069 
-  95%: 0.011163 
-  99%: 0.011207
+  avg: 0.011059 
+  min: 0.010753 
+  max: 0.011497 
+  75%: 0.011180 
+  95%: 0.011364 
+  99%: 0.011470
 time_appconnect 
-  avg: 0.038964 
-  min: 0.034963 
-  max: 0.049771 
-  75%: 0.040087 
-  95%: 0.045336 
-  99%: 0.048884
+  avg: 0.027334 
+  min: 0.026352 
+  max: 0.030412 
+  75%: 0.027708 
+  95%: 0.029410 
+  99%: 0.030212
 time_pretransfer 
-  avg: 0.039045 
-  min: 0.035040 
-  max: 0.049847 
-  75%: 0.040165 
-  95%: 0.045420 
-  99%: 0.048961
+  avg: 0.027415 
+  min: 0.026431 
+  max: 0.030487 
+  75%: 0.027790 
+  95%: 0.029486 
+  99%: 0.030287
 time_ttfb 
-  avg: 0.068345 
-  min: 0.058978 
-  max: 0.077074 
-  75%: 0.073894 
-  95%: 0.076083 
-  99%: 0.076876
+  avg: 0.055659 
+  min: 0.047318 
+  max: 0.069526 
+  75%: 0.060904 
+  95%: 0.066898 
+  99%: 0.069000
 time_total 
-  avg: 0.077203 
-  min: 0.067808 
-  max: 0.085864 
-  75%: 0.082664 
-  95%: 0.084787 
-  99%: 0.085649
+  avg: 0.064454 
+  min: 0.056316 
+  max: 0.078088 
+  75%: 0.069705 
+  95%: 0.075654 
+  99%: 0.077601
 
 time_dns
 avg:,min:,max:,75%:,95%:,99%:
-0.002420,0.002315,0.002544,0.002446,0.002516,0.002538
+0.002403,0.002067,0.002853,0.002515,0.002718,0.002826
 time_connect
 avg:,min:,max:,75%:,95%:,99%:
-0.011064,0.010938,0.011218,0.011069,0.011163,0.011207
+0.011059,0.010753,0.011497,0.011180,0.011364,0.011470
 time_appconnect
 avg:,min:,max:,75%:,95%:,99%:
-0.038964,0.034963,0.049771,0.040087,0.045336,0.048884
+0.027334,0.026352,0.030412,0.027708,0.029410,0.030212
 time_pretransfer
 avg:,min:,max:,75%:,95%:,99%:
-0.039045,0.035040,0.049847,0.040165,0.045420,0.048961
+0.027415,0.026431,0.030487,0.027790,0.029486,0.030287
 time_ttfb
 avg:,min:,max:,75%:,95%:,99%:
-0.068345,0.058978,0.077074,0.073894,0.076083,0.076876
+0.055659,0.047318,0.069526,0.060904,0.066898,0.069000
 time_total
 avg:,min:,max:,75%:,95%:,99%:
-0.077203,0.067808,0.085864,0.082664,0.084787,0.085649
+0.064454,0.056316,0.078088,0.069705,0.075654,0.077601
```