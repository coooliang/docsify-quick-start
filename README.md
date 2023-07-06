
# Infer静态代码分析

## Install 方式1

```
brew install autoconf automake cmake opam pkg-config sqlite gmp mpfr java

# Checkout Infer
git clone https://github.com/facebook/infer.git
cd infer
# Compile Infer
# ./build-infer.sh java
./build-infer.sh clang
# install Infer system-wide...
sudo make install
# ...or, alternatively, install Infer into your PATH
export PATH=`pwd`/infer/bin:$PATH
```

## Install 方式2
[或下载release版本](https://github.com/facebook/infer/releases/download/v1.0.0/infer-osx-v1.0.0.tar.xz)

主执行目录是`infer-osx-v1.0.0/lib/infer/infer/bin/`

[iOS静态分析Infer的使用](https://www.jianshu.com/p/b6204ed62510)
```
open ~/.bash_profile
export PATH="${PATH}:/Users/zjh48/Documents/infer-osx-v1.0.0/lib/infer/infer/bin"
source ~/.bash_profile

infer --version
```

## 命令

`--keep-going 忽略错误继续运行`

`xcode --> clean `
```
infer --keep-going --no-xcpretty -- xcodebuild -workspace YinYin.xcworkspace -scheme yypt -configuration Debug -sdk iphoneos
```

## 添加忽略配置 .inferconfig
[OCaml](https://v2.ocaml.org/api/Str.html)
```
{
  "report-blacklist-path-regex": [
    "Pods",
    "YinYin/Librarys"
  ]
}
```

## Error

```
XCODEBUILD: ** BUILD FAILED **
XCODEBUILD: 
XCODEBUILD: 
XCODEBUILD: The following build commands failed:
XCODEBUILD: 	CompileC /Users/lion/Library/Developer/Xcode/DerivedData/YinYin-dttpfhhhqaogbrdkjnwfiermelko/Build/Intermediates.noindex/YinYin.build/Debug-iphoneos/yypt.build/Objects-normal/arm64/XHLaunchAdConfiguration.o /Users/lion/qd-ios/YinYin/Utils/XHLaunchAd/XHLaunchAd/XHLaunchAdConfiguration.m normal arm64 objective-c com.apple.compilers.llvm.clang.1_0.compiler (in target 'yypt' from project 'YinYin'
XCODEBUILD: 	CompileC /Users/lion/Library/Developer/Xcode/DerivedData/YinYin-dttpfhhhqaogbrdkjnwfiermelko/Build/Intermediates.noindex/YinYin.build/Debug-iphoneos/yypt.build/Objects-normal/arm64/QDSMSCodeView.o /Users/lion/qd-ios/YinYin/Utils/QDNumberKeyBoard/QDSMSCodeView.m normal arm64 objective-c com.apple.compilers.llvm.clang.1_0.compiler (in target 'yypt' from project 'YinYin')
XCODEBUILD: 	CompileC /Users/lion/Library/Developer/Xcode/DerivedData/YinYin-dttpfhhhqaogbrdkjnwfiermelko/Build/Intermediates.noindex/YinYin.build/Debug-iphoneos/yypt.build/Objects-normal/arm64/SARepeatFlushInterceptor.o /Users/lion/qd-ios/YinYin/Librarys/SensorsAnalyticsSDK/Core/Interceptor/Flush/SARepeatFlushInterceptor.m normal arm64 objective-c com.apple.compilers.llvm.clang.1_0.compiler (in target 'yypt' from project 'YinYin')
XCODEBUILD: 	CompileC /Users/lion/Library/Developer/Xcode/DerivedData/YinYin-dttpfhhhqaogbrdkjnwfiermelko/Build/Intermediates.noindex/YinYin.build/Debug-iphoneos/yypt.build/Objects-normal/arm64/pinyin.o /Users/lion/qd-ios/YinYin/Utils/pinyin/pinyin.c normal arm64 c com.apple.compilers.llvm.clang.1_0.compiler (in target 'yypt' from project 'YinYin')
XCODEBUILD: (4 failures)
External Error: *** capture failed to execute: exited with code 65
Error backtrace:
Raised at Stdlib.input_line.scan in file "stdlib.ml", line 456, characters 14-31
Called from Stdio__In_channel.input_line_exn in file "src/in_channel.ml" (inlined), line 64, characters 13-30
Called from IBase__Utils.with_channel_in in file "src/base/Utils.ml", line 277, characters 11-44
Re-raised at IBase__Die.raise_error.do_raise in file "src/base/Die.ml", line 26, characters 8-56
Called from Integration__Driver.capture in file "src/integration/Driver.ml", line 246, characters 10-40
Called from IBase__Utils.timeit in file "src/base/Utils.ml", line 472, characters 16-20
Called from IBase__ScubaLogging.execute_with_time_logging in file "src/base/ScubaLogging.ml", line 83, characters 26-41
Called from Backend__GCStats.log_f in file "src/backend/GCStats.ml", line 93, characters 10-14
Called from Dune__exe__Infer.run in file "src/infer.ml", line 21, characters 2-36
Called from IBase__Utils.timeit in file "src/base/Utils.ml", line 472, characters 16-20
Called from IBase__ScubaLogging.execute_with_time_logging in file "src/base/ScubaLogging.ml", line 83, characters 26-41
Called from Dune__exe__Infer.run in file "src/infer.ml", line 27, characters 22-94
```

1. ToolChains选择 Xcode

2. 删除爱加密相关配置

```
Other C Flags
OTHER_CFLAGS = -mllvm -ipo -mllvm -cxf -mllvm -icf -mllvm -idc -mllvm -equ -fembed-bitcode

Other C++ Flags
$(OTHER_CFLAGS)
```


PS:

[https://github.com/facebook/infer/blob/main/INSTALL.md](https://github.com/facebook/infer/blob/main/INSTALL.md)

[https://fbinfer.com/docs/man-infer](https://fbinfer.com/docs/man-infer)

[https://www.cnblogs.com/ZachRobin/p/11280499.html](https://www.cnblogs.com/ZachRobin/p/11280499.html)

[https://www.jianshu.com/p/dfb04cf2961d](https://www.jianshu.com/p/dfb04cf2961d)


[https://github.com/facebook/infer/issues/1478](https://github.com/facebook/infer/issues/1478)

[https://freegeektime.com/100024501/87477/](https://freegeektime.com/100024501/87477/)