# filebeat ARM 32-bit binary

## Usage
Download the x86 release and replace the `filebeat` executable.  
```
wget https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-7.9.0-linux-x86.tar.gz
tar xzvf filebeat-7.9.0-linux-x86.tar.gz
rm filebeat-7.9.0-linux-x86.tar.gz
cd filebeat-7.9.0-linux-x86
wget https://github.com/a-sync/filebeat-arm32/raw/7.9.0/build/filebeat -O filebeat
chmod +x filebeat
```

## Build
### Start an immutable Go container for cross-compilation
```
docker run -it --rm -v `pwd`:/build golang:latest /bin/bash
```

### Inside the container
```
go get github.com/elastic/beats
cd /go/src/github.com/elastic/beats/filebeat/
git checkout -b v7.9.0
GOARCH=arm go build
cp filebeat /build
exit
```

### Verify the output file
```
file filebeat
#filebeat: ELF 32-bit LSB executable, ARM, EABI5 version 1 (SYSV), statically linked, not stripped
```
