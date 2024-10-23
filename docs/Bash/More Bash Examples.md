### Add text to all files

```bash
#option 1
for filename in *.md; do
	echo "for loop test" >> "$filename";
 done
 
# option 2
echo "my text" | tee -a *.md
```
Named after the T-splitter in plumbing, `tee` "splits" to the standard output and the file to write to. The `-a` is for append, rather than overwrite. So the for loop and this command do the same thing, `tee` just prints out "my text" on top of appending the files. 

### For Loop

```bash
for i in {1..5}
do
   echo "Welcome $i times"
done
```

### Make three files and search all with grep , then remove

```bash
touch testfile1; echo I am file 1 > testfile3
touch testfile2; echo I am file 2 > testfile2
touch testfile3; echo I am file 3 > testfile3
touch testfile4; echo I am file 4 > testfile4
# OR
for i in 1 2 3 4
do
  touch "testfile${i}"
  echo "I am file ${i}" > "testfile${i}"
done

grep file testfile1 testfile2 testfile3

rm -v testfile*
#OR
rm -v te?tf?l?*
# ? is a single character wildcard
```

### Cat (concatonate)

```bash
#concatonate files
echo "This is file1." > file1.txt
echo "This is file2." > file2.txt
cat file1.txt file2.txt > combined.txt

#print to stdout
cat combined.txt
```
`cat` can both be used to concatenate files or print to standard out (stdout), which is where you see it more commonly used.

### While loop

Simple CPU monitor that prints out the load average every 3 seconds continuously.

```bash
while true; do
clear
cat /proc/loadavg
sleep 3 
```

### && vs ;

- semicolon runs sequentially
- && runs only if the previous on succeeds
```bash
asdlkfjaaasldkfqwkler ; pwd
# will run

alasdfjanmsdqwuer && pwd 
# will NOT run
```

### Pretty Colors

Green
```
echo -e "\033[32;1mHello"
```
Red
```
echo -e "\033[31;1mHello"
```

### Downloading

- `tar`: only supports .tar files
	- historically from tape archive, the name somehow stuck
- `wget`: World Wide Web get
	- primarily for downloading
- `curl`: Client URL
	- supports more protocols than wget (SCP, SFTP, SMB)
	 - often considered better for scripting due to its return codes and more output options.
	 - can download and upload
- `dpkg`: Debian packages
	- for .deb packages on Debian systems (Ubuntu, Linux Mint) 
-  `apt`: advanced package tool
	  - will install all dependencies, not just single package
