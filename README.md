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

Recommended: declare the repository in an external libraries catalog
(e.g. `ext-libs.yml` in the test suite conf directory) and pass it to
`dispatcher.sh --ext-libs=ext-libs.yml`:

```yaml
repositories:
  - name: tsf_wifi
    url: <repo URL>
    ref: <tag>
    libs:
      - tapi_cfg_wifi
      - ta_wifi
```

Then bind the libraries to platforms in `builder.conf`:

```
TE_EXT_REPO_USE([tsf_wifi], [], [tapi_cfg_wifi])
TE_EXT_REPO_USE([tsf_wifi], [<agent platform>], [])
TE_TA_TYPE([<ta type>], [<agent platform>], [unix],
           [...], [], [], [], [... tapi_cfg_wifi ta_wifi])
```

Alternatively, without a catalog, declare everything in `builder.conf`:

```
TE_EXT_REPO([tsf_wifi], [], [<repo URL>], [<tag>], [tapi_cfg_wifi])
TE_EXT_REPO([tsf_wifi], [<agent platform>], [<repo URL>], [<tag>],
            [tapi_cfg_wifi ta_wifi])
```

Requires TE with `TE_EXT_REPO` support (the `te_vec_tokenize_string`
helper from lib/tools is also needed by the UCI parser).
