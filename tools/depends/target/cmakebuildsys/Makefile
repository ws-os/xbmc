-include ../../Makefile.include

VERSION.TXT := $(CMAKE_SOURCE_DIR)/version.txt
APP_NAME=$(shell awk '/APP_NAME/ {print tolower($$2)}' $(VERSION.TXT))

ifeq ($(Configuration),)
  Configuration = Release
  ifeq ($(DEBUG_BUILD),yes)
    Configuration = Debug
  endif
endif

ifeq ($(ENABLE_WAYLAND),yes)
  CMAKE_EXTRA_ARGUMENTS = -DCORE_PLATFORM_NAME=wayland -DWAYLAND_RENDER_SYSTEM=gl
endif

BUILD_DIR=$(CMAKE_SOURCE_DIR)/build

all:
	mkdir -p $(BUILD_DIR)
	cd $(BUILD_DIR); $(CMAKE) -DCMAKE_BUILD_TYPE=$(Configuration) -DENABLE_INTERNAL_CROSSGUID=OFF -DENABLE_INTERNAL_FFMPEG=OFF $(CMAKE_EXTRA_ARGUMENTS) $(CMAKE_SOURCE_DIR)

kodi:
	$(MAKE) -C $(BUILD_DIR)

install:
	$(MAKE) -C $(BUILD_DIR) install

clean:
	$(MAKE) -C $(BUILD_DIR) clean

distclean:
	cd $(BUILD_DIR) && rm -rf *
