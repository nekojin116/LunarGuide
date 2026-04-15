## Prerequisites

Install all of the following before starting (do remember to include them in your PATH, if the installers doesn't do it for you):

| Tool                                              | Where to get it |
| ------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Go 1.24+**                                      | https://go.dev |
| **Python 3**                                      | https://python.org |
| **Java (JDK)**                                    | https://adoptium.net |
| **apktool**                                       | https://apktool.org |
| **Android build tools** (`apksigner`, `zipalign`) | Install Android Studio → SDK Manager → SDK Tools → "Android SDK Build-Tools" (probably would not recommend personally, since it has some funky folder name requirements). Alternatively the entire Android Studio package since it comes bundled with a emulator. |
| **protoc**                                        | https://github.com/protocolbuffers/protobuf/releases — download the zip for your OS, extract anywhere, and add to PATH |
| Make                                              | https://sourceforge.net/projects/gnuwin32/files/make/3.81/make-3.81.exe/download?use_mirror=sf-eu-introserv-1&download -->  Install and add to path |
| Terminal                                          | https://apps.microsoft.com/detail/9n0dx20hk701?hl=en-US&gl=MA |

Then install the Python dependencies:

```bash
pip install pycryptodome msgpack lz4
```

And the Go protobuf plugins (run these once):

```bash
go install google.golang.org/protobuf/cmd/protoc-gen-go@latest
go install google.golang.org/grpc/cmd/protoc-gen-go-grpc@latest
```
