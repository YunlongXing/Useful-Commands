```bash
$ sudo apt install clang-11 llvm-11
$ pip install wllvm
$ sudo cp ~/.local/bin/* /bin

$ sudo update-alternatives --remove-all clang
$ sudo update-alternatives --install /usr/bin/clang++ clang++ /usr/bin/clang++-11 100
$ sudo update-alternatives --install /usr/bin/clang clang /usr/bin/clang-11 100
$ sudo update-alternatives --install /usr/bin/llvm-link llvm-link /usr/bin/llvm-link-11 100

$ sudo apt install flex
$ sudo apt install bison
$ sudo apt install libelf-dev
$ sudo apt install libssl-dev

$ clang --version
$ export LLVM_COMPILER=clang
$ make CC=wllvm defconfig
# build Linux kernel with llvm toochain
$ make CC=wllvm -j$(nproc)

# extract bitcode from vmlinux
$ extract-bc vmlinux
$ llvm-dis-11 vmlinux.bc
```

compile openssl into bytecode with asan enabled
```bash
$ export LLVM_COMPILER=clang
$ ./config -fPIC no-shared enable-asan
$ make CC=wwllvm -j$(nproc)
```
Then in ./apps folder
```bash
$ extract-bc openssl
$ llvm-dis openssl.bc
```
The generated file is named openssl.ll
