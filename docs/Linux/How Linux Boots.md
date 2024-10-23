> 📝️ **Video Transcript**: This is the transcript for a video on my youtube channel. It should still be just as readable as an article, but you can also find the video [here](https://www.youtube.com/watch?v=WlbbRTby4AE).

Understanding the Linux boot process is a complex task, but knowing a few major steps and concepts is possible for anyone. If you inspect your file system at the root level, you'll see you have a boot directory, upon inspecting your block devices, you'll find that it may be a separate partition altogether. Looking at the contents, you'll see each type of file have different versions according to each kernel release. Currently I'm on 6.8.9, my Fedora machine stores two previous versions in case I ever need to roll back a version due to a system breaking kernel update.

After the firmware has check and initialized hardware components with a Power on Self Check, or POST test, it looks for a boot device on a hard drive or SSD where the bootloader, GRUB is stored, which the firmware hands over control to. The next step involves Vmlinuz, which stands for Virtual Memory LINUx gZip, meaning it's a gzip-compressed kernel image. 

If you run `journalctl` with the -boot flag, you can see uncompressing this image into memory is the first step. The next step is initramfs, or initial ram filesystem. This loads a temporary filesystem into memory to load just enough kernel modules to recognize the full kernel in order to mount the real filesystem, begin systemd as the init service, and continue into userspace.

These steps can be viewed in a summarized way with `systemd-analyze` starting with exactly how long the firmware took to initialize the hardware, around 10 seconds, 2 and a half seconds for grub, the bootloader, 1 second for uncompressing the kernel, 5 for loading the temporary filesystem, and 12 seconds for systemd to start up every process necessary for userspace. 

An even better way to graphically visualize each step is the run `systemd-analyze plot` and direct the output towards a created SVG file. Here I open it up with Inkscape and have a comprehensive chart of every process. It looks complicated but as I mentioned, it just starts with firmware, the bootloader, uncompressing the kernel, our temporary filesystem which loads all these necessary modules, and next our very first process, or PID 1, SystemD, which spawns all other processes.

This can be visualized with process tree, where you can see every ongoing process on your machine and it's parents, all eventually spawning from systemd. Also as seen in the pseudo or virtual filesystem proc, which displays each ongoing process as a directory in real time, here we can peak at what's inside.

Keep in mind this video is not comprehensive and I'm leaving out many details of about early hardware stages like BIOS and EUFI, instead I hope to show some useful terminal commands and tips to explore yourself. Probably the most useful thing you can take from this video is the SVG chart created from `systemd-analyze`, which you should spent some time with exploring yourself.


If you like these short videos where I explain a Linux subject leave a comment, like, or subscribe to support more content like it. Thanks for watching.