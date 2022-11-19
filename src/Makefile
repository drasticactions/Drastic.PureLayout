XBUILD=/Applications/Xcode.app/Contents/Developer/usr/bin/xcodebuild
ROOT=$(PWD)
PROJECT_ROOT=$(ROOT)/../external/PureLayout/PureLayout
PROJECT=$(PROJECT_ROOT)/PureLayout.xcodeproj
TARGET_IOS=PureLayout_iOS
TARGET_MAC=PureLayout_Mac
PROJECTNAME=PureLayout
OUTPUT=$(ROOT)/Build
BINDING_PROJECT_IOS=$(ROOT)/PureLayout.Binding/PureLayout.Binding
BINDING_PROJECT_MACOS=$(ROOT)/PureLayout.Binding/PureLayout.Binding.Mac
FRAMEWORKS=$(ROOT)/Frameworks/
FRAMEWORKS_IOS=$(ROOT)/Frameworks/ios
FRAMEWORKS_MAC=$(ROOT)/Frameworks/mac

all: ios mac

ios: iossimulator iosdevice
	cp -R $(FRAMEWORKS_IOS)/iphoneos/$(PROJECTNAME).framework $(FRAMEWORKS_IOS)/$(PROJECTNAME).framework
	rm $(FRAMEWORKS_IOS)/$(PROJECTNAME).framework/$(PROJECTNAME)
	lipo -create -output $(FRAMEWORKS_IOS)/$(PROJECTNAME).framework/$(PROJECTNAME) $(FRAMEWORKS_IOS)/iphoneos/$(PROJECTNAME).framework/$(PROJECTNAME) $(FRAMEWORKS_IOS)/iphonesimulator/$(PROJECTNAME).framework/$(PROJECTNAME)

iossimulator:
	$(XBUILD) ONLY_ACTIVE_ARCH=NO -project $(PROJECT) -target $(TARGET_IOS) -sdk iphonesimulator -configuration Release clean build EXCLUDED_ARCHS="arm64"
	mkdir -p $(FRAMEWORKS_IOS)/iphonesimulator
	mv $(PROJECT_ROOT)/build/Release-iphonesimulator/$(PROJECTNAME).framework $(FRAMEWORKS_IOS)/iphonesimulator

iosdevice:
	$(XBUILD) ONLY_ACTIVE_ARCH=NO -project $(PROJECT) -target $(TARGET_IOS) -sdk iphoneos -configuration Release clean build
	mkdir -p $(FRAMEWORKS_IOS)/iphoneos
	mv $(PROJECT_ROOT)/build/Release-iphoneos/$(PROJECTNAME).framework $(FRAMEWORKS_IOS)/iphoneos

mac:
	$(XBUILD) ONLY_ACTIVE_ARCH=NO SUPPORTS_MACCATALYST=YES -project $(PROJECT) -target $(TARGET_MAC) -sdk macosx -configuration Release clean build 
	mkdir -p $(FRAMEWORKS_MAC)
	mv $(PROJECT_ROOT)/build/Release/$(PROJECTNAME).framework $(FRAMEWORKS_MAC)