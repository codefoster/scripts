Unix Toolbox http://cb.vu/unixtoolbox.xhtml

## List directories and their total size
``` bash
du -sh *  # the h shortens bytes to K, M, G for kilo, meg, gig
du -s * | sort -nr | head -10 # shows the top 10 largest
```

## Reclaim write permission on a directory

``` bash
sudo chown -R <user> <directory>
chmod -R a+w <directory> #add write permission
```

# Unzip a file
``` bash
7z x <file> -o<directory> # the `-o` argument doesn't want a space after it
```

# Zip a directory
``` bash
7z a <archive name> <directory>
```

# Zip a directory and ignore certain folders
``` bash
7z a <archive name> <directory> '-xr!node_modules' '-xr!dist'
```

# see ports in use
``` bash
sudo netstat -tulpn
```

# Making Disk Images (without wasting space)
Refer to http://stackoverflow.com/questions/19355036/how-to-create-an-img-image-of-a-disc-sd-card-without-including-free-space

Pretty good and simple way to deal with this is simply pipe it via gzip, something like this:
``` bash
dd if=/dev/sdb | gzip > backup.img.gz
```

This way your image will be compressed and most likely unused space will be squeezed to almost nothing.
You would use this to restore such image back:
``` bash
cat backup.img.gz | gunzip | dd of=/dev/sdb
```

One note: if you had a lot of files which were recently deleted, image size may be still large (deleting file does not necessarily zeroes underlying sectors). You can wipe free space by creating and immediately deleting large file containing zeros:
``` bash
cd /media/flashdrive
dd if=/dev/zero of=bigfile bs=1M     # let it run and quit by disk full error
rm bigfile
```

# Generate test files
``` bash
count=$1
size=$2

mkdir -p files

for (( i=1; i<=count; i++ ))
do
  fallocate -l $size files/$i
done
```

# Concatenating audio files
``` bash
for f in ./barista-2019-10-19T*.wav
    do echo "file '$f'" >> barista-2019-10-19.txt
done
ffmpeg -f concat -safe 0 -i barista-2019-10-19.txt -c copy barista-2019-10-19.wav
```

# SSH Keys
- It's fine if the key on the remote has a username in the file other than what you're signing in as.

## Generate keys
``` bash
ssh-keygen -t rsa
```

Notes…
- If you need a lot of security, add `-b 4096` to that.
- The randomart is for visual recognition of your key
- The passphrase is an extra layer of security, but it's inconvenient to have to type a passphrase every time you log in.

## Copy the public key to the remote server
``` bash
ssh-copy-id -i ~/.ssh/<keyname> <user>@<host>
```

## Generate a certificate using openssl

``` bash
openssl genrsa -out mykey.pem 2048
openssl req -new -sha256 -key mykey.pem -out mycsr.pem
openssl x509 -req -in mycsr.pem -signkey mykey.pem -out mycert.pem
openssl pkcs12 -export -in mycert.pem -inkey mykey.pem -certfile mycert.pem -out mypfx.pfx
```
