# SPDX-License-Identifier: MIT
# Copyright (C) 2025 Interpretica, Unipessoal Lda. All rights reserved.
#
# External TE library (see TE_EXT_REPO): engine-side WiFi configuration
# TAPI. Built as a shared library on the engine platform and as a static
# library for agent platforms (ta_wifi depends on it).

if get_option('engine')
    build_lib_shared = true
endif
build_lib_static = not get_option('engine') \
    or get_option('agents').split().length() != 0 \
    or get_option('agent-apps').split().length() != 0
install_lib = install_dev

headers += files(
    'tapi_cfg_wifi.h',
)

sources += files(
    'tapi_cfg_wifi.c',
)

te_libs += [
    'tools'
]

# Configurator model of the WiFi subtree, used on the engine side
if get_option('engine')
    install_data(
        files('cm_wifi.yml'),
        install_dir: join_paths(get_option('datadir'), 'cm'),
    )
endif
