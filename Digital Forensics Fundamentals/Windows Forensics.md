As part of the data collection phase, forensic images of the Windows Operating system are taken. These forensic images are bit-by-bit copies of the whole operating system.

Two different categories of forensic images are taken from a Windows OS:

1. Disk Image : The disk images contains all the data present on the storage device of the system. This data is non-volatile, meaning that the disk data would survive even after a restart of the os. 
2. Memory Image: The memory contains data inside the OS RAM. This memory is volatile, meaning the data will get lost after the system is powered off or restarted.  For example, to capture open files, running processes, current network connections..the memory image should be prioritized and taken first from the suspects operating system, otherwise any restart or shutdown of the system would result in all the volatile data getting deleted.

### Tools

Used for disk and memory acquisition and analysis of the Windows OS.

**FTK Imager** - used for taking windows OS disk images.

**Autopsy** - An open-source digital forensics platform. An investigator can import an acquired disk image into this tool and the tool will conduct an extensive analysis of the image. It offers various features during image analysis, including keyword search, deleted file recovery, extension mismatch detection and many more.

**Dumplt** - offers the utility of taking a memory image from a windows OS. This tool creates memory images using a command line interface and afew commands.  The memory image can also be taken in different formats.

**Volatility** - A powerful open-source tool for analyzing memory images. It offers some extremely useful plugins.



PDFINFO - shows pdf metadata

Photo EXIF DATA - EXIF stands for Exchangeable Image File Format; it is a standard for saving metadata to image files. When you take a photo with your smartphone or with a digital camera, plenty of information gets embedded in the image.

The following are examples of metadata that can be found in the original digital images.

- Camera model/smartphone model
- Date and time of image capture
- Photo settings such as focal length, aperture, shutter speed, and ISO settings.

Because smartphones are equipped with a GPS sensor, finding GPS coordinates embedded in the image is highly probable. The GPS coordinates, i.e latitude and longitude, would generally show the place where the photo was taken.

exiftool used to read and write metadata in various file types such as JPEG  images.
