XBUILD=/Applications/Xcode.app/Contents/Developer/usr/bin/xcodebuild
ROOT=$(PWD)
PROJECT_ROOT=$(ROOT)/../external/PureLayout/PureLayout
PROJECT=$(PROJECT_ROOT)/PureLayout.xcodeproj
BUILD_ROOT=$(PROJECT_ROOT)/build
TARGET_IOS=PureLayout_iOS
TARGET_MAC=PureLayout_Mac
TARGET_TVOS=PureLayout_tvOS
PROJECTNAME=PureLayout
OUTPUT=$(ROOT)/Build
FRAMEWORK_PATH=Products/Library/Frameworks/PureLayout.framework
BINDING_PROJECT_IOS=$(ROOT)/PureLayout.Binding/PureLayout.Binding
BINDING_PROJECT_MACOS=$(ROOT)/PureLayout.Binding/PureLayout.Binding.Mac
FRAMEWORKS=$(ROOT)/Frameworks
FRAMEWORKS_IOS=$(ROOT)/Frameworks/ios
FRAMEWORKS_MAC=$(ROOT)/Frameworks/mac
FRAMEWORKS_TVOS=$(ROOT)/Frameworks/tvos

all: iossimulator iosdevice maccatalyst tvossimulator tvosdevice mac xcframework dotnet

build: iossimulator iosdevice maccatalyst tvossimulator tvosdevice mac xcframework dotnet

pack: build nuget

iossimulator:
	$(XBUILD) archive ONLY_ACTIVE_ARCH=NO -project $(PROJECT) -scheme $(TARGET_IOS) -destination="generic/platform=iOS Simulator" -archivePath $(BUILD_ROOT)/simulator.xcarchive -sdk iphonesimulator SKIP_INSTALL=NO BUILD_LIBRARIES_FOR_DISTRIBUTION=YES

iosdevice:
	$(XBUILD) archive ONLY_ACTIVE_ARCH=NO -project $(PROJECT) -scheme $(TARGET_IOS) -destination="generic/platform=iOS" -archivePath $(BUILD_ROOT)/iOS.xcarchive -sdk iphoneos SKIP_INSTALL=NO BUILD_LIBRARIES_FOR_DISTRIBUTION=YES

maccatalyst:
	$(XBUILD) archive ONLY_ACTIVE_ARCH=NO -project $(PROJECT) -scheme $(TARGET_IOS) -destination="generic/platform=macOS,variant=Mac Catalyst" -archivePath $(BUILD_ROOT)/catalyst.xcarchive SKIP_INSTALL=NO BUILD_LIBRARIES_FOR_DISTRIBUTION=YES

tvossimulator:
	$(XBUILD) archive ONLY_ACTIVE_ARCH=NO -project $(PROJECT) -scheme $(TARGET_TVOS) -archivePath $(BUILD_ROOT)/tvsimulator.xcarchive -sdk appletvsimulator SKIP_INSTALL=NO BUILD_LIBRARIES_FOR_DISTRIBUTION=YES

tvosdevice:
	$(XBUILD) archive ONLY_ACTIVE_ARCH=NO -project $(PROJECT) -scheme $(TARGET_TVOS) -archivePath $(BUILD_ROOT)/tvos.xcarchive -sdk appletvos SKIP_INSTALL=NO BUILD_LIBRARIES_FOR_DISTRIBUTION=YES

mac:
	$(XBUILD) archive ONLY_ACTIVE_ARCH=NO -project $(PROJECT) -scheme $(TARGET_MAC) -destination "generic/platform=macOS,name=Any Mac" -archivePath $(BUILD_ROOT)/mac.xcarchive SKIP_INSTALL=NO BUILD_LIBRARIES_FOR_DISTRIBUTION=YES

xcframework:
	rm -rf $(BUILD_ROOT)/PureLayout.xcframework
	$(XBUILD) -create-xcframework -framework $(BUILD_ROOT)/simulator.xcarchive/$(FRAMEWORK_PATH) -framework $(BUILD_ROOT)/tvsimulator.xcarchive/$(FRAMEWORK_PATH) -framework $(BUILD_ROOT)/tvos.xcarchive/$(FRAMEWORK_PATH) -framework $(BUILD_ROOT)/mac.xcarchive/$(FRAMEWORK_PATH) -framework $(BUILD_ROOT)/iOS.xcarchive/$(FRAMEWORK_PATH) -framework $(BUILD_ROOT)/catalyst.xcarchive/$(FRAMEWORK_PATH) -output $(BUILD_ROOT)/PureLayout.xcframework
	rm -rf $(FRAMEWORKS)
	mkdir -p $(FRAMEWORKS)
	mv $(BUILD_ROOT)/PureLayout.xcframework $(FRAMEWORKS)/PureLayout.xcframework

dotnet:
	dotnet build

nuget:
	dotnet pack --configuration Release