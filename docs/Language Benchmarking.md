> 🏃 **TLDR**: Based on these benchmarks and my code to aggregate the CPU seconds column, Go and Java perform the same, C# performs twice as fast as both of them, Rust outperforms C# by a small margin. Python is 10x slower than Go or Java.

My favorite bench marking is the [Computer Language Benchmarks Game](https://benchmarksgame-team.pages.debian.net/benchmarksgame/box-plot-summary-charts.html) created by Debian developers. They test physics and astronomy simulations (N-body), various matrix algorithms, binary trees, regex, and more. Though you can do your best to interpret their [mean results](https://benchmarksgame-team.pages.debian.net/benchmarksgame/box-plot-summary-charts.html). I have written some awk and sed to provide another simpler metric comparing one language to another. 

Take this this data comparing Go and Python which I've copied directly from the [website](https://benchmarksgame-team.pages.debian.net/benchmarksgame/fastest/go-python3.html). 

```
fannkuch-redux
source 	secs 	mem 	gz 	cpu secs
Go #3
	8.25 	10,936 	969 	32.92
Go
	11.83 	11,128 	900 	47.26
Go #2
	11.89 	12,708 	896 	47.47
Python 3 #6
	913.87 	11,080 	385 	913.83
Python 3 #4
	285.20 	14,264 	950 	1,123.47
n-body
source 	secs 	mem 	gz 	cpu secs
Go #3
	6.36 	11,244 	1200 	6.37
Go
	6.55 	11,244 	1310 	6.56
Go #2
	6.94 	11,244 	1215 	6.95
Python 3
	383.12 	11,096 	1196 	383.11
Python 3 #2
	402.59 	11,096 	1242 	402.57 
```

### Processing the Data

I only care about the `secs` to measure CPU time. So that means I can remove the names of the algorithms as well as the headers that include `source`, `secs`, etc. A single mention of `source` will remove the each entire record. Though there are none above, there are some tests that fail, we'll remove those and the line above them that contain `Python` or `Go`.

```
/source\|binary\|reverse\|nucleotide\|fasta\|regex\|pidigits\|mandelbrot\|spectral\|n-body\|fannkuch/d
N; /Timed\|Bad\|Failed/{d;}; P; D
```

Now before I run my awk script to average out the first numbered field, I want to make sure `Python` and `Go` are on the same record as the numbers. In vim, `J` will remove a newline, basically moving current selected line up one. Let's run that on every line. Also the test numbers `#3` I want to remove as well as the `3` after Python. That will make it easier for awk to read just the data we want.

```
:g/^/normal J
:%s/#.//g
```

After all that our data should look much cleaner.

```
Go 33.37 	247,824 	525 	60.85
Go 34.62 	236,728 	482 	61.41
Python 104.73 	271,980 	338 	104.72
Python 35.33 	274,884 	660 	125.79
```

Now using awk I simply take the second field and average them for Go and Python separately.

```
awk '/Python/{python_sum+=$2; python_count++} /Go/{go_sum+=$2; go_count++} END{print "Python Average: " (python_sum/python_count); print "Go Average: " (go_sum/go_count)}' go-python.txt
```

### Final Results

Here is the result. I've also included some other languages as well. First I compare Go to three other languages, then C# against Java and Go in the last two. Not surprising to see Go 10x faster than Python, though I was shocked to see C# performed 2-3x faster than Go and Java. 

```
Python Average: 106.756
Go Average: 8.98625

Java Average: 9.0565
Go Average: 8.98625

Rust Average: 3.06823
Go Average: 8.98625

C# Average: 3.74485
Java Average: 9.0565

C# Average: 3.74485
Go Average: 8.98625
```
