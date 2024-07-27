# MonkeyDev修改支持巨魔越狱开发  -----  公众号XLsnow

## 很多人不会theos开发, 只喜欢Xcode开发, 但MonkeyDev已多年没有更新, 
## 故做些许修改, 支持打包编译Tweak开发, 支持iOS15-16的无根越狱Rootless


这是一个为越狱和非越狱开发人员准备的工具，主要包括四个模块:
## Logos Tweak

使用theos提供的logify.pl工具将*.xm文件转成*.mm文件进行编译，集成了CydiaSubstrate，可以使用MSHookMessageEx和MSHookFunction来Hook OC函数和指定地址。

## CaptainHook Tweak

使用CaptainHook提供的头文件进行OC 函数的Hook以及属性的获取。

## Command-line Tool

可以直接创建运行于越狱设备的命令行工具

## MonkeyApp

这是自动给第三方应用集成Reveal、Cycript和注入dylib的模块，支持调试dylib和第三方应用，支持Pod给第三放应用集成SDK，只需要准备一个砸壳后的ipa或者app文件即可。


1. 第一步还是安装Theos, 因为插件都是需要他的, MonkeyDev只是套壳

安装最新的theos
sudo git clone --recursive https://github.com/theos/theos.git /opt/theos
新增Xcode--Build Setting里--MonekDevRootless  为 YES 无根 或 NO 有根
设置Xcode对应编译的处理器 arm64 A11-  ||||    arm64e A12+


# 修改MonkeyDev的开发templates
## 执行以下命令 MonkeyDevRootless=YES CODE_SIGNING_ALLOWED=NO
```
sudo /usr/libexec/PlistBuddy -c "Add :Targets:0:SharedSettings:MonkeyDevRootless string YES"  ~/Library/Developer/Xcode/Templates/MonkeyDev/Base.xctemplate/TemplateInfo.plist

sudo /usr/libexec/PlistBuddy -c "Add :Targets:0:SharedSettings:CODE_SIGNING_ALLOWED string NO"  ~/Library/Developer/Xcode/Templates/MonkeyDev/Base.xctemplate/TemplateInfo.plist

sudo /usr/libexec/PlistBuddy -c "Set :Targets:0:SharedSettings:MonkeyDevDeviceIP localhost"  ~/Library/Developer/Xcode/Templates/MonkeyDev/Base.xctemplate/TemplateInfo.plist

sudo /usr/libexec/PlistBuddy -c "Set :Targets:0:SharedSettings:MonkeyDevDevicePassword alpine"  ~/Library/Developer/Xcode/Templates/MonkeyDev/Base.xctemplate/TemplateInfo.plist

sudo /usr/libexec/PlistBuddy -c "Set :Targets:0:SharedSettings:MonkeyDevDevicePort 2222"  ~/Library/Developer/Xcode/Templates/MonkeyDev/Base.xctemplate/TemplateInfo.plist

sudo /usr/libexec/PlistBuddy -c "Set :Targets:0:SharedSettings:MonkeyDevkillProcessOnInstall "  ~/Library/Developer/Xcode/Templates/MonkeyDev/Base.xctemplate/TemplateInfo.plist
```
