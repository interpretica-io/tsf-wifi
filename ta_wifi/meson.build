# SPDX-License-Identifier: MIT
# Copyright (C) 2025 Interpretica, Unipessoal Lda. All rights reserved.
#
# External TE library (see TE_EXT_REPO): agent-side WiFi configuration
# subtree. Linked wholly into agents so that the constructor in
# ta_wifi_conf_ext.c registers the subtree without Test Agent
# modifications.

link_whole = true

headers += files(
    'ta_wifi.h',
)

sources += files(
    'ta_wifi.c',
    'ta_wifi_conf_ext.c',
    'ta_wifi_internal.c',
    'ta_wifi_uci.c',
    'ta_wifi_uci_apply.c',
    'ta_wifi_uci_parser.c',
    'ta_wifi_wh.c'
)

te_libs += [
    'agentlib',
    'rpc_types',
    'tools',
    'rcfpch',
    'tapi_cfg_wifi',
]
