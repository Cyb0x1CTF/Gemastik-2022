### Challenge Information
| Variable       | Value              |
|:---------------|:-------------------|
| Challenge Name | Where is my flag?? |
| Category       | Forensics          |
| Points         | 350                |
| Difficulty     | Medium             |

### Description
Disajikan sebuah file berekstensi `.jpg` yang berisi gambar, namun dari gambar tersebut tidak dapat dilihat apapun selain gambar gedung biasa

![](profile.jpg)

Resource file: [profile.jpg](profile.jpg)

### Solution
#### Percobaan 1
Pada percobaan pertama, dilakukan pengecekan dengan menggunakan `binwalk` untuk melihat apakah terdapat file lain yang tersembunyi di dalam file gambar tersebut. Hasilnya adalah tidak ada file lain yang tersembunyi di dalam file gambar tersebut.
```bash
$ binwalk profile.jpg

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             JPEG image data, JFIF standard 1.01
14153         0x3749          JPEG image data, JFIF standard 1.01
```

#### Percobaan 2
Pada percobaan kedua, dilakukan pengecekan metadata dari file gambar tersebut dengan menggunakan `exiftool`. Hasilnya adalah tidak ada metadata yang tersembunyi di dalam file gambar tersebut.
```bash
$ exiftool profile.jpg
ExifTool Version Number         : 12.42
File Name                       : profile.jpg
Directory                       : .
File Size                       : 18 kB
File Modification Date/Time     : 2022:10:22 22:03:01+07:00
File Access Date/Time           : 2022:10:24 08:26:00+07:00
File Inode Change Date/Time     : 2022:10:24 08:25:58+07:00
File Permissions                : -rw-r--r--
File Type                       : JPEG
File Type Extension             : jpg
MIME Type                       : image/jpeg
JFIF Version                    : 1.01
Resolution Unit                 : inches
X Resolution                    : 96
Y Resolution                    : 96
Comment                         : CREATOR: gd-jpeg v1.0 (using IJG JPEG v62), default quality.
Image Width                     : 350
Image Height                    : 240
Encoding Process                : Baseline DCT, Huffman coding
Bits Per Sample                 : 8
Color Components                : 3
Y Cb Cr Sub Sampling            : YCbCr4:2:0 (2 2)
Image Size                      : 350x240
Megapixels                      : 0.084
```

#### Percobaan 3
Pada percobaan ketiga, dilakukan ekstraksi file yang tersembunyi di dalam file gambar tersebut dengan menggunakan `stegoveritas`. Stegoveritas merupakan tools untuk melakukan ekstraksi file yang tersembunyi di dalam file gambar. Hasilnya 
```bash
$ stegoveritas profile.jpg
Running Module: SVImage
+------------------+------+
|   Image Format   | Mode |
+------------------+------+
| JPEG (ISO 10918) | RGB  |
+------------------+------+
Found something worth keeping!
MPEG ADTS, layer III, v2, Monaural
Trailing Data Discovered... Saving
b'\xff\xd8\xff\xe0\x00\x10JFIF\x00\x01\x01\x01\x00`\x00`\x00\x00\xff\xdb\x00C\x00\x03\x02\x02\x03\x02\x02\x03\x03\x03\x03\x04\x03\x03\x04\x05\x08\x05\x05\x04\x04\x05\n\x07\x07\x06\x08\x0c\n\x0c\x0c\x0b\n\x0b\x0b\r\x0e\x12\x10\r\x0e\x11\x0e\x0b\x0b\x10\x16\x10\x11\x13\x14\x15\x15\x15\x0c\x0f\x17\x18\x16\x14\x18\x12\x14\x15\x14\xff\xdb\x00C\x01\x03\x04\x04\x05\x04\x05\t\x05\x05\t\x14\r\x0b\r\x14\x14\x14\x14\x14\x14\x14\x14\x14\x14\x14\x14\x14\x14\x14\x14\x14\x14\x14\x14\x14\x14\x14\x14\x14\x14\x14\x14\x14\x14\x14\x14\x14\x14\x14\x14\x14\x14\x14\x14\x14\x14\x14\x14\x14\x14\x14\x14\x14\x14\xff\xc0\x00\x11\x08\x002\x00\xe9\x03\x01"\x00\x02\x11\x01\x03\x11\x01\xff\xc4\x00\x1f\x00\x00\x01\x05\x01\x01\x01\x01\x01\x01\x00\x00\x00\x00\x00\x00\x00\x00\x01\x02\x03\x04\x05\x06\x07\x08\t\n\x0b\xff\xc4\x00\xb5\x10\x00\x02\x01\x03\x03\x02\x04\x03\x05\x05\x04\x04\x00\x00\x01}\x01\x02\x03\x00\x04\x11\x05\x12!1A\x06\x13Qa\x07"q\x142\x81\x91\xa1\x08#B\xb1\xc1\x15R\xd1\xf0$3br\x82\t\n\x16\x17\x18\x19\x1a%&\'()*456789:CDEFGHIJSTUVWXYZcdefghijstuvwxyz\x83\x84\x85\x86\x87\x88\x89\x8a\x92\x93\x94\x95\x96\x97\x98\x99\x9a\xa2\xa3\xa4\xa5\xa6\xa7\xa8\xa9\xaa\xb2\xb3\xb4\xb5\xb6\xb7\xb8\xb9\xba\xc2\xc3\xc4\xc5\xc6\xc7\xc8\xc9\xca\xd2\xd3\xd4\xd5\xd6\xd7\xd8\xd9\xda\xe1\xe2\xe3\xe4\xe5\xe6\xe7\xe8\xe9\xea\xf1\xf2\xf3\xf4\xf5\xf6\xf7\xf8\xf9\xfa\xff\xc4\x00\x1f\x01\x00\x03\x01\x01\x01\x01\x01\x01\x01\x01\x01\x00\x00\x00\x00\x00\x00\x01\x02\x03\x04\x05\x06\x07\x08\t\n\x0b\xff\xc4\x00\xb5\x11\x00\x02\x01\x02\x04\x04\x03\x04\x07\x05\x04\x04\x00\x01\x02w\x00\x01\x02\x03\x11\x04\x05!1\x06\x12AQ\x07aq\x13"2\x81\x08\x14B\x91\xa1\xb1\xc1\t#3R\xf0\x15br\xd1\n\x16$4\xe1%\xf1\x17\x18\x19\x1a&\'()*56789:CDEFGHIJSTUVWXYZcdefghijstuvwxyz\x82\x83\x84\x85\x86\x87\x88\x89\x8a\x92\x93\x94\x95\x96\x97\x98\x99\x9a\xa2\xa3\xa4\xa5\xa6\xa7\xa8\xa9\xaa\xb2\xb3\xb4\xb5\xb6\xb7\xb8\xb9\xba\xc2\xc3\xc4\xc5\xc6\xc7\xc8\xc9\xca\xd2\xd3\xd4\xd5\xd6\xd7\xd8\xd9\xda\xe2\xe3\xe4\xe5\xe6\xe7\xe8\xe9\xea\xf2\xf3\xf4\xf5\xf6\xf7\xf8\xf9\xfa\xff\xda\x00\x0c\x03\x01\x00\x02\x11\x03\x11\x00?\x00\xfdS\xa2\x8a(\x00\xa2\x8a(\x00\xa2\x8a(\x00\xa2\x8a(\x00\xa2\x8a(\x00\xa2\x8a(\x00\xa2\x8a(\x00\xa2\x8a(\x00\xa2\x8a(\x00\xa2\x8a(\x00\xa2\x8a(\x00\xa2\x8a(\x00\xa2\x8a(\x00\xa2\x8a(\x00\xa2\x8a(\x00\xaf$\xf1W\x8f|e\xe2/\x8a\x97\x9e\x02\xf0\x14\x9a\x1e\x936\x8f\xa7[\xeaz\xc6\xbb\xaf\xd9M\x7f\x1c\x7fhi\x96\x0bh\xad\xa2\x9a\x02\xce|\x87vs0\x08\xbbF\xd6/\x95\xf5\xba\xf0\x8f\x8a\x1f\x04\xf5\xcdG\xe2\x06\xb7\xe2=\x13D\xf0\xa7\x8d\xf4o\x13\xe9v\xbaf\xbd\xe1?\x19\xcf$\x16\x92\xb5\xac\x92Ims\x1c\x8bor\t\x1ek+F\xd0\xe0\xe1\x182\x95\xc1\x89;Y\xda\xff\x00\xf0\xce\xdf\x8f\xe3\xbe\x97)l\xfe_\x9a\xbf\xe1\x7f\xd3[\x1d\xaf\x8a~3\xe8_\x0cm4\xebo\x19^H5\xc9-\x1a\xea\xe6\xdb@\xd2\xefu/.4\xc0\x92\xe1\xa3\x82)\x1e\x18\x03\x7f\xcbI\x00Q\xd3q"\xb3|M\xfbQ\xfc.\xf0\x8e\xabm\xa7j^,\x84\\\xdc\xdb[^C\xf6KY\xee\xa3xn7\xfd\x9d\xc4\x91F\xc9\x89J\x15C\x9f\x9d\x8a\xaa\xe5\x99A\xf1\x1d?\xf6E\xf1\x7f\x86t\xff\x00\x05\xdc[5\xae\xb9{a\xe0\xfb\x1f\x0cjZ]\xaf\x8e5\x8f\x0c\xdb\xc6\xf6\xcd#,\xb1\\X\xc6Zto:E1\xcb\x12\xe3\n\xc0\x8c\xb2\x9d\xa9?d\xddb\xd7\xc4V\x17:,Z.\x85\xa2ZG\xe1\x08\xe0\xd2\xc6\xa1stm\x93J\xba\xb9\x9a\xe25\x95\xe2\xdd \xdb:,n\xd8.T\x96\tZ\xb5\xae\xff\x00j\xdf+\xb5\x7f\xba\xcfK\xae\x84K\xddM\xc7[F\xeb\xcd\xd9i\xf7\xddk\xae\x87\xad\xea\x1f\xb4\x7f\x80\xb4\xef\x08\xe9>&\x1a\x8e\xa5\x7f\xa3\xeav\x86\xfe\tt\xad\n\xfe\xfaD\xb7\x19\xdd,\xd0\xc1\x03\xc9\x02\x02\x08-*\xa0\x04\x10y\x04V\x87\x89\xbe9x7\xc2\xc9\xa3\x19o\xef5w\xd6-M\xf5\x84>\x1c\xd2o5\x99g\xb6\x1b\x7f\xd2\x04vqJ\xc2/\x9d\x07\x98@RX\x0c\xe4\xd7\xcfm\xfb/\xfcU\xb1\xf0\x9f\x85\xbc9o\xad\xd8^i6\x1a\x04\xdad\x96v\xde-\xd5\xb4Hl\xef\xa4\xb8\x91\xcd\xe6,\xa3W\xbe_-\xe3_&W\x88\x0f,\xeda\xbd\x9a\xba_\x15~\xcf~,\x9b\xe1\xa7\xc3\xfd\x07I\xd14I\xfcQ\xe1\xdf\rG\xa3\x8f\x16[\xf8\xc7R\xd0\xaf,f\x10\xa4m\xe4\x9b[Fk\x887"\xc9\xe5\xca\xea\x8cQw\'q\x1d\x1b\xf3\xd1y{\xde\x8a\xfa-tZ\xfd\xd4\xd5\xa4\x95\xfaj\xfc\xfd\xdf\xf3~zv\xd5\xf7\x1f\x13\xbfi\xcd\x17\xe1\x87\x8f<\x1d\xe1\xab\xad\x07\xc4\x9a\x81\xd7\xdeO2\xea\xc7\xc3\xda\x9d\xc0\xb7E\xb7y\x94\xa2\xc3j\xfe{\x92\x9bZ$;\xe3\x04\xb3\x00\x01\xa3\xe2\xd7\xc7)<+k\xe0\x07\xd1\x18i\xe7\xc4Z\xce\x9fo$\xde#\xf0\xee\xae!\x16\x93\xcc\xb14e\xa2\x83\x16\xb7LdE\x8dnLcq\xf9\x87\x06\x9f\xf1\x1b\xe1\xb7\x8d5\x1f\xf8V\x1a\xee\x89y\xa4\xf8\x87\xc5^\x0e\xb9i\xae\x97Z\x95\xf4\xeb}S\xcc\xb2\x92\xdag\xf3!\x8ac\x0b\x16q \x026^\n\xf1\xc1\x19\x7f\x1e<\x1f\xf1K\xe2W\x85\xfc/\xa6\xe8\xde\x1f\xf0\x84sZ\xeazV\xb9~\xd7\xde%\xba\x8dc\xb8\xb4\xbc\x8e\xe5\xad\xe2\xdb\xa7?\x98\x8d\xe5m\x12\xb6\xc27g\xcb\xe3\x06\xd7*\x9co\xb2\x92\xbf\xf8o\xaf\xe1\xfeV\xd5\x10\xae\xe2\xdd\xb5\xe5\x7f}\x9f\xeb\xfew\xd1\x9b\x9e*\xf8\xe1o\xe0_\x8b\x1a\xd6\x8f\xe2+\xbd?I\xf0\x86\x97\xe1H\xf5\xf9\xf5)\xc3\x89RF\xbaxv\xe7v\x18\x10\xaa\x15B\xee,p3\x90*/\x8a\xde6\xf1\xcd\x9f\x81\xee\xfcg\xe0\xbb\xcf\x0e\xe9\x1e\x1f\xd3\xb4I\xf5\x99\x97\xc5\x9aM\xef\xda\xae\x8a!\x90B\xd1\x19-\xda\xcc\x05^^A#\x02\xfc\xc4\xbb>~+\xe2\x7f\xec\xdb\xe2o\x8a\x9f\x12\xb4\xbf\x882\xdei~\x1e\xf16\x8d\xa1Z\x8d&8o\'\xbd\xb4\xb6\xd5\xe1\xb9\x92o\xde\xc6\xd1\xc6\xb7\x16\xe5\\\xc7\xbd\x95d]\xcc\xc8#`\x1a\xac|l\xf8s\xf1c\xe2\xd3xKN\xbc\xd0|\x19\xa9x>\x08R\xf3\xc4>\x1b\x9b\xc4\xd7\x96\x89\xa8\xdf\xabe!i\x97O\x90\xcbf\x84\x07(Q\x0c\x8d\xb47\xca\xa5_\x14\xa4\xe9\xa4\xdd\xa5w\xe7\xa5\xe5f\xfb\xe9k/%}\x1e\x9a\xde*\xa3v\xbcl\xbf(\xdd.\xda\xdf_7kr\xebW\xc5_\xb4\x87\x89u{\x11s\xe1\x87\xf0\xff\x00\x83\xe1\xb1\xf0\xae\x9f\xe2MBo\x17\xd9\xdc]o\x9e\xf8\xc8-4\xe8\x92)a"Vh\x99K\x83#nx\xd5bb\xd8\xadmW\xe3\x07\x8e\xfc[\xf0?N\xf8\xa3\xe0\xf3\xe1\xaf\x0c\xe8\xa3\xc3/\xaf\xdd\xd9x\xa2\xd2\xe2\xeaw\x99b25\xaec\x9a\x05\xb7U\xd8\xc0\xcc|\xd2K\x7f\xaa]\xbf5\x1f\x16|\x13\xf1\xb5\xcf\xc5\x8d?\xe2\x8e\x8d\xa2x>\xef\xc53h\t\xa5\\i\xba\xd6\xadr\xd6z5\xd4m!\x8a\xf2\xceE\xb5>s\x04\x9eX\xc8h\xa1b\xa7\x0b"\x06pr<q\xfb;\xf8\xed\xbc)\xf0\xef\xe1\xee\x8dk\xe1\xcf\x16\xfc2\xf0\xee\x9f\x00\xd5\xb4\xeds\\\xba\xd2\xe7\xd7/b#g\x9f\xe5\xd9\xdc\x83m\xb8y\xad\x16F\xf7*\x18\xecB\xaf\xa4\xbd\xeen_v\xefN\xb6\xf8\xbe\xfb.W\xd9\xe8\xb7\xe7"\x1a4\xe7\xaaI_\xa5\xf4\x8d\xfd\x1d\xf9\xbc\xd5\xdfE\x13\xb6\xf1\xb7\xc4o\x887\x9f\t\xed~!\xf8U\xbc5\xe1\xad"\x1f\x0c\x9f\x10\xddY\xf8\xa2\xd2\xe2\xeay\x1f\xc8\xf3\xbe\xccLs@\xb6\xea\xaa\x083\x1f4\x92\xdf\xea\xc6\xcf\x99\xde<\xf8\x91\xaex\x93\xe1\xdf\xc2\xeb\x8f\x0f\xde]\xf82\xfb\xc7z\x96\x9f\x03\xdc,0\xcdy\xa7\xc3-\xb4\x97R\xack4o\x19\x93l%2\xf1\xb0\x00\xb3m\xc8\x18\xc2\xf8\xdd\xf0\xe7\xe2\x9f\xc5\x89<)\xa6\xcd\xe1\xef\x06\xdfx&\x08\x96\xf3^\xf0\xc5\xc7\x89\xee\xedR\xfe\xf5_1\xc0\xf3.\x9d\'\x9df\x98\x0eP\xa4fF\xda\x18\x05R\xafg\xe3S\xdbx.o\x86\x9f\x12|Ce\xa4\xf8GW\xb1\xd6-t\xff\x00\x10k\x96WE\xa1\xb4\xd3\xa5\x8eu6\xf3^4q3\xday\xef\t\xfd\xe2\xaa\x07(\xc5T\x80Cn<\xdd\x93\x9cl\xbb.n\xfdS\xba^QW\xdd\xb4%u\x1e\xedB_7\xcb\xa7\xcdj\xfc\xdb\xb6\xcbMo\x17~\xd0\x9aw\xc2\xcf\x8a\x8f\xe1?\x12\xdd\xcd>\x9f\x17\x86\xe0\xd5"\x92\xcfK\xb9\xbf\xd4\xae$\xf3\xa6\x8ei\x0c6\x91\xb91\xaa\xc6\x8c\xcc\xb1\x05B\xfc\x90\n\x8a\xa3\xfbC~\xd1\x97\x1e\x06\xf8S\x06\xb7\xf0\xe9t\xcf\x13k\xda\xa6\x93s\xae\xe9\x8du\xbeK!\xa7[\xdb\xfd\xa2k\xb9<\xb2\xacc\xd8c\x8dp\xc32O\x10\xce\t\xc5\xff\x00\x17xo\xc7\xd2|S\x93\xc6\xde\x01\xb5\xf0\xae\xb5\xa7j\x9e\x1a\x83J\x13\xea\xfa\xcc\xf6\xa6\x16Y\xe6\x95gE\x8a\xd6e\x9d\n\xcc\xa7\x1b\xe3\xce:\x8c\xe6\xb8=w\xf6\'\xba\xb7\xf8c\xa9h\x9e\x1a\xf8\x95\xe2+\x1db_\x05\xa7\x84\x95e\x8fO671\xc7\x0c\x8a\xaa\xfem\x9c\xd3\xc3\x1b\xc9+3\x88\xa4\x07\x04`\xe5W\x19\xaeog\xefow\xff\x00\xa5O\xf4\xe4\xed\xa3\xd3U\xa6\xd0\xe4\xf6\xab\xf9t\xfc\xa3}\x7f\xf0\'\xd7U\xad\x96\xfd\x1f\x8c\xbfi\x1d_\xc2\xbf\x11\xee<+o\xa4\xd9\xea\xfa\x85\xe7\x86t\xdb\xed\x0fM\x87z\\_jwS\xddFbg\xcb\x05\x81\x12\xdf\xccv\xdb\x94D\x95\x89 \x01]\xee\xad\xf1j\xc7\xe1\xae\x9f\xa0\xe9\x9e6\xbd\x97S\xf1u\xe5\xa1\x9ak_\tx{P\xbf2l\xda%\x95-\xad\xd6\xe2X\xe1\x0c\xea\xa1\x9c\xe3$\r\xd98\xaf*\xd5\x7fd\xbd_W\xf1\xd2x\x9e\xe3\xc5\x1fh\xf1\x16\x97\xe1[-3A\xf1]\xccP\x9dN\xc7Q\x86\xe6\xe6V\x90\xacPE\x11\xb7d\x99"tP<\xc8\xc3\xab\x0ew\x1do\x8b\x9f\x0b|y\xf1+F\xf0\xfd\xd8\xf0\xbf\x86\xed|qo\xa6Ko\'\x88\xb4\xbf\x1b\xea\x9a<\xdal\xf2\x00\x19m\xde\xde\xcc\xbd\xcc\x1b\x95$\xf2\xa6eR\xca\x01S\x8d\xd5\xa4\xb4Zj\xee\xfe\xeb\xca\xd6\xdb\xa5\xb7i[\x94\xc2:\xb5~\xd1\xfb\xf9c\xcd\x7f+\xedmo\xccX\xf8\xbb\xf1\xbb\xc4zO\x88u\xbd3\xc2\xb7\xfe\x1d\xf0\xfd\xb7\x87\xf4;mb\xff\x00Q\xf1]\x85\xcc\xebu5\xd4\x92\xc7gc\x0cQ\xcb\x0b,\x8e\xd00-\x99\x1bs\xc6\x8b\x133b\xbd;\xe1\x1f\xc4(\xbe,|1\xf0\xbf\x8ca\xb1\x9bLMkO\x86\xf4\xd8\xdc\x7f\xac\xb7gPZ6\xe0d\xabdg\x038\xe8+\xc7\xfcU\xf0\x0f\xc6V_\x14\xb4\x9f\x88z\x11\xf0\xdf\x8c|P\xbe\x1c\x87E\xb9\x9f\xc53\xcde\x15\xad\xec[\xf6\xeav\xf1\xc3\x0c\xcada4\xea\xd1\xe1\x0e\xd6\xda\xb2\xa8g\x07\xa5\xf0\xaf\xc4o\x84\xdf\xb3\x9f\x84\xf4/\x86\xfa\xef\xc5O\ni\xba\xaf\x87\xb4\xfb{9\xe2\xd6\xb5\xcb[K\xb7a\x1a\x9f5\xe2\x92]\xc8_;\xf0{0\xc6E\n\xc9I_\xae\x9f|\xbfN^\x8b\xa7^`\xd6M;t\xfd#\xfa\xdf\xf1\xe9\xcab\xf8\xd3\xf6\x92\xd5|\x15\xf1\xbb\xc5^\x13\xb8\xd3ln4;/\x0eEy\xa5\xcc\xa1\xd6\xe6\xe3Vo1\x96\xcd\x89m\xa4J\x8a\nm\x00\xe5$\xc9<c\x98\xf17\xedQ\xe3-\x1f\xf6d\xd0|Og\xa4\xe8w\x9f\x13\xf5-&\xfbT\x96\xc5Rs\xa6\xdb\xc3b\xae\xf7\x97,7\xf9\x9eP\xd8\x91\xa8.\t\x92x\x86q\x92;\xff\x00\x05\xf8\'\xc2\x9f\x14\xbck\xe2?\x1fC\xaa\xe8>5\xf0\xf5\xf6\xa1\xa6\xdfh\xb7\xda>\xa1\xf6\x95\x86\xe2\xca\x19"$\xbcga*\xf2I\x85\x0c\xc3\xe69\x00\xd7\x9aK\xfb\x16\xf8\x8eo\x86\xfe-\xb5\x87\xe2\x1e\xa5\xa3\xf8\xabZ\xd1\xf5\x1d\x1cZ\xd8\x8b)t\xb7\x82[\x8b\xb9\xa0\x89\xde{\x19.#F\xfbO\xef|\xa6RNv\xfd\xd5#7\xcc\x95\xbf\xae\xad}\xed\xdb\xfc)u5\xa7\xca\xea\'-\xbf\xe1\x97\xe0\x95\xd7\x9d\xef\xa1\xea\x1f\x19\xbe#x\xcf\xc0\xda/\x81\xfcE\xa2\xddhCK\xd45\x8d#K\xd4\xf4\xeb\xfd2i\xa7\x90^\xdeA\x03<\x13\xa5\xca,E\x16V 4rd\x81\xd2\xbb?\x88\x7f\x17\xbc3\xf0\xba4}zmH\xee\x89\xee\x194\xad\x1a\xf3Sxa_\xbd,\xa9k\x14\x8d\x14c\x9f\x9d\xc0^\x08\xcf\x15\xe5\xbf\x16~\x15\xfcN\xd6\xbc\x03\xe0\xff\x00\t\xe8\x0f\xa2\xf8\xa4i\x1a\x8e\x97\xab]k\x9e*\xd6\x9a\xc2\xe6i,\xefc\xb9\xf2DV\x9akFU\x84A\x04\x83i\x19\xc9F \x96\xaf\xf1\x9b\xe1/\xc5_\x89\x9a\xe6\x9fy\x05\xdd\x85\xb6\x996\x82l\xa7\xd1\xad\xbci\xabiP\xe9\xba\x8b\xb9/t\xafe\x0co\xa8&\xc2\xaa"\x98\xc2?vq\xb3\xccb4\xa8\xed\x19rk\xefJ\xde\x9c\xaa\xdf|\x93K\xd7\xa2\xb1\x9d%~_h\xfe\xcco\xeb}\x7f\x06\x9b\xfd^\x86\xa4\xbf\xb4E\xf3~\xd0\x91\xf8N\xcd4\xadC\xc17\x9e\x1b\xb4\xd4\xac\xb5kb\xcf+\xdd\xdc}\xaeH\xbep\xe5\x1a\x06\x8a\xcd\xf1\x80\x0e\xe6_\x98\xe7\x14\xbe\x0f\xfd\xab<=o\xf0w\xc0\xde)\xf1\xbd\xc4\xb6\xba\xce\xb9\xe1\xe8\xf5\xeb\xbb?\x0f\xe8\xd7\xda\x80\xb7\x87b\x99fh\xed\xe3\x99\xe1\x81Kc|\x84/m\xc4\x83\\\xd6\x81\xfb-\xf8\x8fO\xd2g\x86\xe7P\xd2\x05\xf4>\x07\xf0\xfe\x87a<o#\x88uM6I\xe5Y\x881\x8f\xdc\xf9\x8f\x16\x08\xf9\x88\x0e\n\x8e\xfe\t\xe3-\x1bR\xf85\xe2\x0f\t\xf87R\xf1\xde\x81\xe0\xadCK\xf8oa\xa2j\xb7\x1a\x87\x8a-\xfc?i\xabG\xe7N$\x8e\xde\xe2\xe7M\xbb{\x9d\xbbO\xfa\xb4\x82H\xbc\xcc\x86&\\"\xa9h9F/\xae\x8d\xf6^\xd1\xfe\x91\xbf\x95\xad\xd8\xa8\xfb\xcb\x9eK\xa4n\xbc\xdf"\x7f\x9b\xb7\x9d\xcf\xab>%|F\xbd\x8fB\xf8}\xf1\x0f\xc2\xfe#\xd4-|9}\xaci\xb6W\x1aE\xf6\x9a\x96\xf6\xf7\xd6\xb7\xb7)o\xe6\xca\xb3\xc0\xb70\xbay\xaa\xe8C\xa0$\r\xca\xc1\xab\xdb+\xe5\xff\x00\x15|B\xd2\xfcQ\xf0O\xe1\x17\x86\xadl\xa5\xf0\x8e\xab\xe2\xcb\xbd\x16(\xbc\r=\xc9\x17\xed\xa6\xa4\xf1\x1b\xb8Ly\x12In\xb6\xe9 \x91\x99@1\xe48\x1b\x8a\xd7\xd2\xbaN\x91c\xe1\xfd.\xcfL\xd2\xec\xad\xf4\xdd6\xce\x15\xb7\xb6\xb3\xb4\x89b\x86\x08\xd4\x05TDP\x02\xa8\x00\x00\x00\xc0\x02\xb5\x94TT\xd2\xe96\x97{Z?\x93\xfcn\xba\x19)6\xe3}\xdcSv\xdbyk\xf3\xfc\xad\xdc\xb7E\x14VF\x81E\x14P\x01E\x14P\x01E\x14P\x01E\x14P\x01E\x14P\x01E\x14P\x01E\x14P\x01E\x14P\x01E\x14P\x01E\x14P\x01E\x14P\x01E\x14P\x01E\x14P\x01E\x14P\x01E\x14P\x01E\x14P\x01E\x14P\x01E\x14P\x01E\x14P\x01E\x14P\x01E\x14P\x01E\x14P\x01E\x14P\x01E\x14P\x01E\x14P\x01E\x14P\x01E\x14P\x01E\x14P\x01E\x14P\x01E\x14P\x07\xff\xd9'
Running Module: MultiHandler

Found something worth keeping!
JPEG image data, JFIF standard 1.01, resolution (DPI), density 96x96, segment length 16, comment: "CREATOR: gd-jpeg v1.0 (using IJG JPEG v62), default quality", baseline, precision 8, 350x240, components 3
Exif
====
+---------------------+--------------------------------------------------------------------------------------+
| key                 | value                                                                                |
+---------------------+--------------------------------------------------------------------------------------+
| SourceFile          | /Users/macbookair/CTF/Gemastik2022/Warm-Up/challenges/Where is my flag??/profile.jpg |
| ExifToolVersion     | 12.42                                                                                |
| FileName            | profile.jpg                                                                          |
| Directory           | /Users/macbookair/CTF/Gemastik2022/Warm-Up/challenges/Where is my flag??             |
| FileSize            | 18 kB                                                                                |
| FileModifyDate      | 2022:10:22 22:03:01+07:00                                                            |
| FileAccessDate      | 2022:10:24 08:26:00+07:00                                                            |
| FileInodeChangeDate | 2022:10:24 08:25:58+07:00                                                            |
| FilePermissions     | -rw-r--r--                                                                           |
| FileType            | JPEG                                                                                 |
| FileTypeExtension   | jpg                                                                                  |
| MIMEType            | image/jpeg                                                                           |
| JFIFVersion         | 1.01                                                                                 |
| ResolutionUnit      | inches                                                                               |
| XResolution         | 96                                                                                   |
| YResolution         | 96                                                                                   |
| Comment             | CREATOR: gd-jpeg v1.0 (using IJG JPEG v62), default quality                          |
|                     |                                                                                      |
| ImageWidth          | 350                                                                                  |
| ImageHeight         | 240                                                                                  |
| EncodingProcess     | Baseline DCT, Huffman coding                                                         |
| BitsPerSample       | 8                                                                                    |
| ColorComponents     | 3                                                                                    |
| YCbCrSubSampling    | YCbCr4:2:0 (2 2)                                                                     |
| ImageSize           | 350x240                                                                              |
| Megapixels          | 0.084                                                                                |
+---------------------+--------------------------------------------------------------------------------------+
```

Setelah mengekstrak file `profile.jpg` didapatkan sebuah file bernama `trailing_data.bin`, lalu dilakukan pengecekan pada metadata dari file tersebut dengan menggunakan `exiftool`

```bash
$ exiftool trailing_data.bin
ExifTool Version Number         : 12.42
File Name                       : trailing_data.bin
Directory                       : .
File Size                       : 3.9 kB
File Modification Date/Time     : 2022:10:24 08:57:11+07:00
File Access Date/Time           : 2022:10:24 08:58:15+07:00
File Inode Change Date/Time     : 2022:10:24 08:57:11+07:00
File Permissions                : -rw-r--r--
File Type                       : JPEG
File Type Extension             : jpg
MIME Type                       : image/jpeg
JFIF Version                    : 1.01
Resolution Unit                 : inches
X Resolution                    : 96
Y Resolution                    : 96
Image Width                     : 233
Image Height                    : 50
Encoding Process                : Baseline DCT, Huffman coding
Bits Per Sample                 : 8
Color Components                : 3
Y Cb Cr Sub Sampling            : YCbCr4:2:0 (2 2)
Image Size                      : 233x50
Megapixels                      : 0.012ftool trailing_data.bin
```

Karena dari meta data didapatkan informasi bahwa file tersebut merupakan file `JPEG` maka file tersebut diubah menjadi file `JPEG` dengan menggunakan perintah `mv trailing_data.bin trailing_data.jpg`
Berikut adalah isi dari file `trailing_data.jpg`

![](trailing_data.jpg)

Flag sudah didapatkan, selanjutnya ambil teks dari gambar tersebut dengan menggunakan `tesseract` dikarenakan kami sangat teramat malas sekali untuk menulis ulang teks tersebut

```bash
$ tesseract trailing_data.jpg flag
$ cat flag.txt
Gemastik2022({b4Ks®_M4laNg}
```

Semalas-malasnya kami, tetapi kami tidak malas untuk mengganti `®` menjadi `0` maka flag yang benar adalah
```
Gemastik2022{b4Ks0_M4laNg}
```