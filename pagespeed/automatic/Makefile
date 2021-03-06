#
# Copyright 2011 Google Inc.
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#      http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
#
# Author: jmarantz@google.com (Joshua Marantz)

# This Makefile provides a mechanism to generate a Page Speed Automatic
# library (.a) from an already-built mod_pagespeed distribution.  This

# MOD_PAGESPEED_ROOT should be set to the 'src' directory where mod_pagespeed
# was built.  See:
# https://developers.google.com/speed/pagespeed/module/build_from_source
#
# When running this Makefile from the 'automatic' directory then it will
# be set automatically.
MOD_PAGESPEED_ROOT = $(shell cd ../..; pwd)

# OUTPUT_ROOT should be set to wherever you want to put output files.  Default
# is to put them in the current directory.
OUTPUT_DIR = $(PWD)

# You can use a Debug or a Release build.  Default is Release.  Feel free
# to set this to Debug to get visibility into Page Speed Automatic code.
#
# Note that this is the same Makefile variable used by the generated Makefiles
# on Linux.
BUILDTYPE = Release

# TODO(jmarantz): this library-list should be automatically generated
# from the 'gyp' flow, rather than hand-entered here.
BASE_LIBS = \
  base/libbase.a \
  base/libbase_static.a \
  build/libwebp_dec.a \
  build/libwebp_dsp.a \
  build/libwebp_enc.a \
  build/libwebp_enc_mux.a \
  build/libwebp_mux.a \
  build/libwebp_utils.a \
  net/instaweb/libautomatic_util.a \
  net/instaweb/libinstaweb_add_instrumentation_data2c.a \
  net/instaweb/libinstaweb_add_instrumentation_opt_data2c.a \
  net/instaweb/libinstaweb_admin_site_css_data2c.a \
  net/instaweb/libinstaweb_apr.a \
  net/instaweb/libinstaweb_automatic.a \
  net/instaweb/libinstaweb_caches_css_data2c.a \
  net/instaweb/libinstaweb_caches_js_data2c.a \
  net/instaweb/libinstaweb_caches_js_opt_data2c.a \
  net/instaweb/libinstaweb_client_domain_rewriter_data2c.a \
  net/instaweb/libinstaweb_client_domain_rewriter_opt_data2c.a \
  net/instaweb/libinstaweb_console_css_data2c.a \
  net/instaweb/libinstaweb_console_js_data2c.a \
  net/instaweb/libinstaweb_console_js_opt_data2c.a \
  net/instaweb/libinstaweb_critical_css_beacon_data2c.a \
  net/instaweb/libinstaweb_critical_css_beacon_opt_data2c.a \
  net/instaweb/libinstaweb_critical_css_loader_data2c.a \
  net/instaweb/libinstaweb_critical_css_loader_opt_data2c.a \
  net/instaweb/libinstaweb_critical_images_beacon_data2c.a \
  net/instaweb/libinstaweb_critical_images_beacon_opt_data2c.a \
  net/instaweb/libinstaweb_critical_images_pb.a \
  net/instaweb/libinstaweb_critical_keys_pb.a \
  net/instaweb/libinstaweb_dedup_inlined_images_data2c.a \
  net/instaweb/libinstaweb_dedup_inlined_images_opt_data2c.a \
  net/instaweb/libinstaweb_defer_iframe_data2c.a \
  net/instaweb/libinstaweb_defer_iframe_opt_data2c.a \
  net/instaweb/libinstaweb_delay_images_data2c.a \
  net/instaweb/libinstaweb_delay_images_inline_data2c.a \
  net/instaweb/libinstaweb_delay_images_inline_opt_data2c.a \
  net/instaweb/libinstaweb_delay_images_opt_data2c.a \
  net/instaweb/libinstaweb_dependencies_pb.a \
  net/instaweb/libinstaweb_deterministic_data2c.a \
  net/instaweb/libinstaweb_deterministic_opt_data2c.a \
  net/instaweb/libinstaweb_extended_instrumentation_data2c.a \
  net/instaweb/libinstaweb_extended_instrumentation_opt_data2c.a \
  net/instaweb/libinstaweb_flush_early_pb.a \
  net/instaweb/libinstaweb_graphs_css_data2c.a \
  net/instaweb/libinstaweb_graphs_js_data2c.a \
  net/instaweb/libinstaweb_graphs_js_opt_data2c.a \
  net/instaweb/libinstaweb_input_info_pb.a \
  net/instaweb/libinstaweb_js_defer_data2c.a \
  net/instaweb/libinstaweb_js_defer_opt_data2c.a \
  net/instaweb/libinstaweb_lazyload_images_data2c.a \
  net/instaweb/libinstaweb_lazyload_images_opt_data2c.a \
  net/instaweb/libinstaweb_local_storage_cache_data2c.a \
  net/instaweb/libinstaweb_local_storage_cache_opt_data2c.a \
  net/instaweb/libinstaweb_messages_js_data2c.a \
  net/instaweb/libinstaweb_messages_js_opt_data2c.a \
  net/instaweb/libinstaweb_rendered_image_pb.a \
  net/instaweb/libinstaweb_responsive_js_data2c.a \
  net/instaweb/libinstaweb_responsive_js_opt_data2c.a \
  net/instaweb/libinstaweb_rewriter.a \
  net/instaweb/libinstaweb_rewriter_base.a \
  net/instaweb/libinstaweb_rewriter_css.a \
  net/instaweb/libinstaweb_rewriter_html.a \
  net/instaweb/libinstaweb_rewriter_html_gperf.a \
  net/instaweb/libinstaweb_rewriter_image.a \
  net/instaweb/libinstaweb_rewriter_javascript.a \
  net/instaweb/libinstaweb_rewriter_pb.a \
  net/instaweb/libinstaweb_spriter.a \
  net/instaweb/libinstaweb_spriter_pb.a \
  net/instaweb/libinstaweb_static_asset_config_pb.a \
  net/instaweb/libinstaweb_statistics_css_data2c.a \
  net/instaweb/libinstaweb_statistics_js_data2c.a \
  net/instaweb/libinstaweb_statistics_js_opt_data2c.a \
  net/instaweb/libinstaweb_system.a \
  net/instaweb/libinstaweb_util.a \
  net/instaweb/libprocess_context.a \
  net/instaweb/libtest_infrastructure.a \
  pagespeed/libinstaweb_mobilize_css_data2c.a \
  pagespeed/libinstaweb_mobilize_js_data2c.a \
  pagespeed/libinstaweb_mobilize_js_opt_data2c.a \
  pagespeed/libjs_tokenizer.a \
  pagespeed/libjsminify.a \
  pagespeed/libmem_lock.a \
  pagespeed/libpagespeed_ads_util.a \
  pagespeed/libpagespeed_base.a \
  pagespeed/libpagespeed_base_core.a \
  pagespeed/libpagespeed_base_test_infrastructure.a \
  pagespeed/libpagespeed_cache.a \
  pagespeed/libpagespeed_controller.a \
  pagespeed/libpagespeed_controller_proto.a \
  pagespeed/libpagespeed_html.a \
  pagespeed/libpagespeed_html_gperf.a \
  pagespeed/libpagespeed_http.a \
  pagespeed/libpagespeed_http_core.a \
  pagespeed/libpagespeed_http_gperf.a \
  pagespeed/libpagespeed_http_pb.a \
  pagespeed/libpagespeed_image_processing.a \
  pagespeed/libpagespeed_image_types_pb.a \
  pagespeed/libpagespeed_javascript_gperf.a \
  pagespeed/libpagespeed_logging.a \
  pagespeed/libpagespeed_logging_enums_pb.a \
  pagespeed/libpagespeed_logging_pb.a \
  pagespeed/libpagespeed_opt_http.a \
  pagespeed/libpagespeed_property_cache_pb.a \
  pagespeed/libpagespeed_sharedmem.a \
  pagespeed/libpagespeed_sharedmem_pb.a \
  pagespeed/libpagespeed_thread.a \
  pagespeed/libpthread_system.a \
  pagespeed/libutil.a \
  third_party/apr/libapr.a \
  third_party/aprutil/libaprutil.a \
  third_party/base64/libbase64.a \
  third_party/chromium/src/base/third_party/dynamic_annotations/libdynamic_annotations.a \
  third_party/css_parser/libcss_parser.a \
  third_party/css_parser/libcss_parser_gperf.a \
  third_party/css_parser/libutf.a \
  third_party/domain_registry_provider/src/domain_registry/libassert_lib.a \
  third_party/domain_registry_provider/src/domain_registry/libdomain_registry_lib.a \
  third_party/domain_registry_provider/src/domain_registry/libinit_registry_tables_lib.a \
  third_party/gflags/libgflags.a \
  third_party/giflib/libdgiflib.a \
  third_party/giflib/libgiflib_core.a \
  third_party/grpc/libgpr.a \
  third_party/grpc/libgrpc_core.a \
  third_party/grpc/libgrpc_cpp.a \
  third_party/hiredis/libhiredis.a \
  third_party/icu/libicudata.a \
  third_party/icu/libicuuc.a \
  third_party/jsoncpp/libjsoncpp.a \
  third_party/libjpeg_turbo/libjpeg.a \
  third_party/libjpeg_turbo/src/libjpeg_turbo.a \
  third_party/libpng/libpng.a \
  third_party/optipng/libopngreduc.a \
  third_party/protobuf/libprotobuf_full_do_not_use.a \
  third_party/re2/libre2.a \
  third_party/serf/libopenssl.a \
  third_party/serf/libserf.a \
  third_party/zlib/libzlib.a \
  url/liburl_lib.a

# The 'gclient' build flow uses 'xcodebuild' on Mac and 'make' on Linux.
# To make matters worse, it puts all the intermediate libraries in the same
# directory on Mac but distributes them over a directory tree on Linux.

ifeq ($(HOSTTYPE),intel-mac)

# on MacOS the xcodebuild system puts all the libraries in the same directory
# so we strip it with 'notdir'.
INCLUDE_ARCH = arch/mac/ia32
LIBS = $(addprefix $(MOD_PAGESPEED_ROOT)/xcodebuild/$(BUILDTYPE)/,$(notdir $(BASE_LIBS)))
BINDIR = /Developer/usr/bin
CXX = $(BINDIR)/gcc-4.2 -arch i386 -fvisibility=hidden
SYSLIBS = -Wl,-search_paths_first -framework AppKit -lpthread -lstdc++
TESTBENCH_LIB = $(MOD_PAGESPEED_ROOT)/out/$(BUILDTYPE)/obj.target/libre2_bench_util.a

build_libraries :
	cd $(MOD_PAGESPEED_ROOT)/build && xcodebuild -project all.xcodeproj \
		-configuration $(BUILDTYPE) -target pagespeed_automatic

# TODO(jmarantz): here's a potential egrep expression to make the build less
# noisy.
#		| egrep -v '(BUILD NATIVE|Check dependencies|$^|PhaseScriptExecution|BUILD AGGREGATE|.build/Script-|Nothing to be done for|cd /)'

else

# TODO(jmarantz): test this on 32-bit systems.  Add fail handler for non-linux
# non-mac.
ifeq ($(HOSTTYPE),x86_64-linux)
 INCLUDE_ARCH = arch/linux/x64
else
 INCLUDE_ARCH = arch/linux/ia32
endif
INCLUDE_ARCH = arch/linux/x64
LIBS = $(addprefix $(MOD_PAGESPEED_ROOT)/out/$(BUILDTYPE)/obj.target/, $(BASE_LIBS))
SYSLIBS = -lpthread -lrt
TESTBENCH_LIB = $(MOD_PAGESPEED_ROOT)/out/$(BUILDTYPE)/obj.target/third_party/re2/libre2_bench_util.a

build_libraries :
	cd $(MOD_PAGESPEED_ROOT) && $(MAKE) $(CXXFLAGS_ARG) BUILDTYPE=$(BUILDTYPE)

endif

INCLUDE_PATH = \
    -I$(MOD_PAGESPEED_ROOT) \
    -I$(MOD_PAGESPEED_ROOT)/out/$(BUILDTYPE)/obj/gen/protoc_out/instaweb \
    -I$(MOD_PAGESPEED_ROOT)/third_party/chromium/src \
    -I$(MOD_PAGESPEED_ROOT)/third_party/gflags/gen/$(INCLUDE_ARCH)/include \
    -I$(MOD_PAGESPEED_ROOT)/third_party/google-sparsehash/src \
    -I$(MOD_PAGESPEED_ROOT)/third_party/google-sparsehash/gen/$(INCLUDE_ARCH)/include \
    -I$(MOD_PAGESPEED_ROOT)/third_party/protobuf/src/src \
    -I$(MOD_PAGESPEED_ROOT)/third_party/re2/src
PSOL = $(OUTPUT_DIR)/pagespeed_automatic.a
OBJS          = $(OUTPUT_DIR)/static_rewriter_main.o \
		$(OUTPUT_DIR)/static_rewriter.o \
		$(PSOL)
SPEED_TEST_OBJS = $(TESTBENCH_LIB) \
		$(OUTPUT_DIR)/rewriter_speed_test.o \
		$(OUTPUT_DIR)/static_rewriter.o \
		$(PSOL)
EXE           = $(OUTPUT_DIR)/static_rewriter
SPEED_TEST    = $(OUTPUT_DIR)/rewriter_speed_test
EXAMPLE_ROOT  = $(MOD_PAGESPEED_ROOT)/install/mod_pagespeed_example
EXAMPLES      = $(OUTPUT_DIR)/collapse_whitespace.html
MERGE_LOG     = $(OUTPUT_DIR)/merge.log
RENAME_LOG    = $(OUTPUT_DIR)/rename.log
LOGS          = $(MERGE_LOG) $(RENAME_LOG)

MAKE := $(MAKE) --no-print-directory
exe : $(EXE)
speed_test : $(SPEED_TEST)

# Specifying 'build_libraries' as a dependency but recursively making
# 'static_rewriter' allows 'make -j' to work.  This is needed because
# we don't articulate all the dependencies required to build the libraries.
all : build_libraries
	$(MAKE) examples
	$(MAKE) $(SPEED_TEST)

# Flags used to compile static_rewriter.cc.  Note that these are not
# the flags used to compile pagespeed_automatic, which is compiled
# with either BUILDTYPE=Release or BUILDTYPE=Debug
override CXXFLAGS := $(CXXFLAGS) -std=gnu++0x

$(PSOL) : $(LIBS)
	@echo Merging libraries, logs in $(MERGE_LOG) ...
	@./merge_libraries.sh $@.dirty $(LIBS) > $(MERGE_LOG)
	@echo Cleaning namespace, logs in $(RENAME_LOG) ...
	@./rename_c_symbols.sh $@.dirty $@ > $(RENAME_LOG)
	rm $@.dirty

.PHONY : psol
psol : build_libraries
	$(MAKE) $(PSOL)

# Ideally we want the main .o files to depend on all the headers in PSOL,
# but that's not easy to keep up-to-date.  As a proxy for those, recompile
# .o files whenever the library changes.  This is a little conservative
# because the library might change without any header changes, but recompiling
# the .o files is cheap.
$(OUTPUT_DIR)/%.o : %.cc $(PSOL)
	$(CXX) $(INCLUDE_PATH) $(CXXFLAGS) $(MOD_PAGESPEED_INCLUDE) -c $< -o $@

$(EXE) : $(OBJS)
	$(CXX) $(CXXFLAGS) -o $@ $^ $(SYSLIBS)

$(OUTPUT_DIR)/collapse_whitespace.html : $(EXE) $(EXAMPLE_ROOT)/collapse_whitespace.html
	$(EXE) --rewriters=collapse_whitespace $(EXAMPLE_ROOT) $(OUTPUT_DIR) \
                collapse_whitespace.html

$(SPEED_TEST) : $(SPEED_TEST_OBJS)
	$(CXX) $(CXXFLAGS) -o $@ $^ $(SYSLIBS)

examples : $(EXAMPLES)

clean :
	rm -f $(OUTPUT_DIR)/static_rewriter $(EXE) $(OBJS) $(EXAMPLES) $(LOGS)

echo_libs :
	echo LIBS = $(LIBS)
