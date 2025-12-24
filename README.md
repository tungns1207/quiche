# QUICHE (Modified for Traffic Analysis)

[Origin Repo for instructions](https://github.com/google/quiche)


## Build and run standalone QUICHE

QUICHE has binaries that can run on Linux platforms.

Follow the [instructions](https://bazel.build/install) to install Bazel.

```
sudo apt install libicu-dev clang lld
cd <directory that will be the root of your quiche implementation>
git clone https://github.com/google/quiche.git
cd quiche
CC=clang bazel build -c opt //...
./bazel-bin/quiche/<target_name> <arguments>
```
### Note: The repository includes a demo .pcap file and a key.log file in the certs directory


### 1. Start the proxy
```bash
bazel-bin/quiche/masque_server --certificate_file certs/server.crt --key_file certs/server.key
```

### 2. Set the SSLKEYLOGFILE and start the client
```bash
bazel-bin/quiche/masque_client --disable_certificate_verification=true 127.0.0.1:9661 https://cloudflare-quic.com
```
### 3. Capture using Wireshark and decrypt using the TLS key 

