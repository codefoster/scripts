# Reclaim write permission on a directory

``` bash
sudo chown -R <user> <directory>
chmod -R a+w <directory> #add write permission
```

# Generate a certificate using openssl

``` bash
openssl genrsa -out mykey.pem 2048
openssl req -new -sha256 -key mykey.pem -out mycsr.pem
openssl x509 -req -in mycsr.pem -signkey mykey.pem -out mycert.pem
openssl pkcs12 -export -in mycert.pem -inkey mykey.pem -certfile mycert.pem -out mypfx.pfx
```

# Unzip a file
7z x <file> -o<directory> # the `-o` argument doesn't want a space after it
7z a <archive name> ./<directory>/*
