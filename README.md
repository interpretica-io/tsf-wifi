# tsf-wifi

WiFi configuration support for the OKTET Labs Test Environment (TE),
packaged as an external TE repository (consumed with the `TE_EXT_REPO`
builder directive).

Libraries:

- `tapi_cfg_wifi` — engine-side TAPI for the `/agent/wifi` configuration
  subtree (shared library, plus the `cm_wifi.yml` configurator model
  installed to `share/cm`);
- `ta_wifi` — agent-side implementation of the subtree with two
  backends: UCI (OpenWrt) and hostapd/wpa_supplicant. Registers itself
  via `TE_RCF_PCH_CONF_EXT()`, no Test Agent modification is needed.

## Usage

In your `builder.conf`:

```
TE_EXT_REPO([tsf_wifi], [], [<repo URL>], [<tag>], [tapi_cfg_wifi])
TE_EXT_REPO([tsf_wifi], [<agent platform>], [<repo URL>], [<tag>],
            [tapi_cfg_wifi ta_wifi])
TE_TA_TYPE([<ta type>], [<agent platform>], [unix],
           [...], [], [], [], [... tapi_cfg_wifi ta_wifi])
```

Requires TE with `TE_EXT_REPO` support (the `te_vec_tokenize_string`
helper from lib/tools is also needed by the UCI parser).
