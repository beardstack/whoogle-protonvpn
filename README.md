
## [Whoogle-Search](https://github.com/benbusby/whoogle-search) search proxied through [ProtonVPN Docker](https://github.com/tprasadtp/protonvpn-docker) and served through [traefik](https://github.com/traefik/traefik)


<img src="https://protonvpn.com/assets/img/protonvpn-transparent.svg" height="20%" width="20%"> <img src="https://github.com/benbusby/whoogle-search/raw/main/docs/banner.png" height="20%" width="20%"> <img src="https://github.com/authelia/authelia/raw/master/docs/static/images/authelia-title.png" height="20%" width="20%"> <img src="https://github.com/traefik/traefik/raw/master/docs/content/assets/img/traefik.logo.png" height="15%" width="15%"> <img src="https://github.com/containrrr/watchtower/raw/main/logo.png" height="10%" width="10%"> 

### Objectives:
1. Defend against propaganda that could be forcibly distributed based on location
1. Easy bootstrap compose file to spawn service quickly with sensible defaults
1. Make it harder to track users for marketing and advertising
1. Use docker for isolation/containerization
1. Use docker best practices.
1. Learn



The compose file runs a protonvpn client that will route traffic from the whoogle container.

### Requirements
The compose file assumes a few things:
1. You have a protonvpn account
1. Traefik is the reverse proxy/edge router
1. Traefik is configured with an entrypoint named "websecure"
1. Traefik is configured with a TLS resolver named myresolver


It also supports via labels
- Restarting ProtonVPN service through [Chadburn](https://github.com/PremoWeb/chadburn) `CHADBURN_ENABLED=true`
- Authentication assuming you have [Authelia](https://github.com/authelia/authelia) running with `AUTHELIA_MIDDLEWARE` configured
- Automatic updates through [watchtower](https://github.com/containrrr/watchtower) `WATCHTOWER_ENABLED=true`


### Variable definitions

| VARIABLE                       | Required? | Default        |                                                                               |
|--------------------------------|-----------|----------------|-------------------------------------------------------------------------------|
| APP_SVC_NAME                   | No        | whoogle        | sets the base name for the container                                          |
| HOST_NAME                      | **YES**   | -              | FQDN e.g example.com                                                          |
| APP_PORT                       | No        | 5000           |                                                                               |
|                                |           |                |                                                                               |
| PROTONVPN_USERNAME             | **YES**   | -              | Needed to establish connection to proton                                      |
| PROTONVPN_PASSWORD             | **YES**   | -              | Needed to establish connection to proton                                      |
| PROTONVPN_TIER                 | **YES**   | -              | Needed to establish connection to proton                                      |
| PROTONVPN_CHECK_INTERVAL       | No        | 10             | How often the connection to Proton will be tested                             |
| PROTONVPN_FAIL_THRESHOLD       | No        | 3              | How many times can it fail                                                    |
| PROTONVPN_SERVER               | No        | CA             | Pick your server. More [info](https://github.com/tprasadtp/protonvpn-docker)  |
|                                |           |                |                                                                               |
| RESTART_POLICY                 | No        | unless-stopped |                                                                               |
| AUTHELIA_MIDDLEWARE            | No        | -              | Your authelia middleware if applicable                                        |
| WATCHTOWER_ENABLED             | No        | false          | Enable watchtower updates                                                     |
| TRAEFIK_ENABLED                | No        | true           | Enable traefik routing                                                        |
| CHADBURN_ENABLED               | No        | false          | Enables periodically changing VPN servers                                     |
|                                |           |                |                                                                               |
| WHOOGLE_CONFIG_LANGUAGE        | No        | en             |                                                                               |
| WHOOGLE_CONFIG_SEARCH_LANGUAGE | No        | en             |                                                                               |
| WHOOGLE_CONFIG_THEME           | No        | dark           |                                                                               |
| WHOOGLE_CONFIG_ALTS            | No        | true           |                                                                               |
| WHOOGLE_CONFIG_VIEW_IMAGE      | No        | true           |                                                                               |
| WHOOGLE_CONFIG_URL             | **YES**   | -              | URL for your service e.g https://example.com                                  |
| WHOOGLE_CONFIG_STYLE           | No        | -              | css config                                                                    |
| WHOOGLE_CONFIG_DISABLE         | No        | 1              | Disable customization                                                         |
| WHOOGLE_CONFIG_COUNTRY         | No        | US             |                                                                               |
| WHOOGLE_TOR_SERVICE            | No        | 0              | TOR disabled (mostly because rate limiting)                                   |
| WHOOGLE_CONFIG_TOR             | No        | 0              | TOR disabled (mostly because rate limiting)                                   |
|                                |           |                |                                                                               |





