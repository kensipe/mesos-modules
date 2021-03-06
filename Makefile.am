# Licensed to the Apache Software Foundation (ASF) under one
# or more contributor license agreements.  See the NOTICE file
# distributed with this work for additional information
# regarding copyright ownership.  The ASF licenses this file
# to you under the Apache License, Version 2.0 (the
# "License"); you may not use this file except in compliance
# with the License.  You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License

AUTOMAKE_OPTIONS = subdir-objects

MESOS_ROOT_DIR=@MESOS_ROOT@
MESOS_BUILD_DIR=@MESOS_BUILD_DIR@

LIBPROCESS = $(MESOS_ROOT_DIR)/3rdparty/libprocess
STOUT = $(LIBPROCESS)/3rdparty/stout

# Unfortunatley, 'pkglibexecdir' and 'pkgsysconfdir' are not set
# before automake 1.11, so we need to set them manually (until we in
# the future assume an automake version).
pkglibexecdir = $(libexecdir)/$(PACKAGE)
pkgsysconfdir = $(sysconfdir)/$(PACKAGE)

# Initialize variables here so we can use += operator everywhere else.
lib_LTLIBRARIES =

# Add compiler and linker flags for pthreads.
AM_CXXFLAGS = $(PTHREAD_CFLAGS)
AM_LIBS = $(PTHREAD_LIBS)

# Setup CPPFLAGS that are used for most source files.
MESOS_CPPFLAGS = $(AM_CPPFLAGS)
MESOS_CPPFLAGS += -Wall -Werror
MESOS_CPPFLAGS += -DLIBDIR=\"$(libdir)\"
MESOS_CPPFLAGS += -DPKGLIBEXECDIR=\"$(pkglibexecdir)\"
MESOS_CPPFLAGS += -DPKGDATADIR=\"$(pkgdatadir)\"

MESOS_CPPFLAGS += -I$(MESOS_ROOT_DIR)/src
MESOS_CPPFLAGS += -I$(MESOS_ROOT_DIR)/include
MESOS_CPPFLAGS += -I$(MESOS_BUILD_DIR)/src
MESOS_CPPFLAGS += -I$(MESOS_BUILD_DIR)/include
MESOS_CPPFLAGS += -I$(LIBPROCESS)/include
MESOS_CPPFLAGS += -I$(STOUT)/include

MESOS_CPPFLAGS += -I$(MESOS_BUILD_DIR)/include

# Library containing test CPU and memory isolator modules.
lib_LTLIBRARIES += libtestisolator.la
libtestisolator_la_SOURCES = isolator/test_isolator_module.cpp
libtestisolator_la_CPPFLAGS = $(MESOS_CPPFLAGS)
libtestisolator_la_LDFLAGS = -release $(PACKAGE_VERSION) -shared

# Library containing the test CRAM-MD5 authentication modules.
# TODO(tillt): Add cyrus-sasl2 dependency while removing it from libmesos.
# TODO(tillt): Enable optional building of this module library.
# TODO(tillt): Make this module library installable. See MESOS-1940.
lib_LTLIBRARIES += libtestauthentication.la
libtestauthentication_la_SOURCES = authentication/test_authentication_modules.cpp
libtestauthentication_la_CPPFLAGS = $(MESOS_CPPFLAGS)
libtestauthentication_la_LDFLAGS = -release $(PACKAGE_VERSION) -shared

.PHONY: $(PHONY_TARGETS)
