

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

| VARIABLE                       | Required? | Default                |                                                                               |
|--------------------------------|-----------|------------------------|-------------------------------------------------------------------------------|
| APP_SVC_NAME                   | No        | whoogle                | sets the base name for the container                                          |
| HOST_NAME                      | **YES**   | -                      | FQDN e.g example.com                                                          |
| PROTONVPN_USERNAME             | **YES**   | -                      | Neededed to establish connection to proton                                    |
| PROTONVPN_PASSWORD             | **YES**   | -                      | Neededed to establish connection to proton                                    |
| PROTONVPN_TIER                 | **YES**   | -                      | Neededed to establish connection to proton                                    |
| WHOOGLE_CONFIG_URL             | **YES**   | -                      | URL e.g http://example.com                                                    |


| PROTONVPN_WATCHTOWER_ENABLED   | No        | false                  | Enable Auto update for protonvpn image                                        |
| WHOOGLE_WATCHTOWER_ENABLED     | No        | false                  | Enable Auto update for whooglee                                               |

|                                |           |                        |                                                                               |
| TRAEFIK_ENABLED                | No        | true                   |  Enable traefik routing                                                        |
| APP_PORT                       | No        | 5000                   |                                                                               |
| AUTHELIA_MIDDLEWARE            | No        | -                      | Your authelia middleware if applicable                                        |
| CHADBURN_ENABLED               | No        | false                  | Enables periodically changing VPN servers                                     |
| CHADBURN_SCHEDULE              | No        | @hourly                | How often the reconnect command will execute                                  |
| CHADBURN_COMMAND               | No        | protonvpn connect --sc | How often the reconnect command will execute                                  | 



| PROTONVPN_IMAGE                | No        | tprasadtp/protonvpn    | Build your own image bro                                                      |
| PROTONVPN_VERSION              | No        | latest                 | YOLO                                                                          |
| PROTONVPN_CHECK_INTERVAL       | No        | 10                     | How often the connection to Proton will be tested                             |
| PROTONVPN_FAIL_THRESHOLD       | No        | 3                      | How many times can it fail                                                    |
| PROTONVPN_IPCHECK_ENDPOINT     | No        | https://icanhazip.com/ | Where to query to get your IP                                                 |
| PROTONVPN_SERVER               | No        | RANDOM                 | Pick your server. More [info](https://github.com/tprasadtp/protonvpn-docker)  |
| PROTONVPN_DNS_LEAK_PROTECT     | No        | 1                      | Enabled by default                                                            |
| PROTONVPN_PROTOCOL             | No        | udp                    | TCP or UDP                                                                    |
| PROTONVPN_DEBUG                | No        | 0                      | Change to 1 to see get more verbose                                           |
| PROTONVPN_RESTART_TRIES        | No        | 5                      | How many times to attempt restart                                             |
| EXCLUDE_CIDR                   | No        | -                      | You should leave that as is                                                   |

| WHOOGLE_IMAGE                  | No        | benbusby/whoogle-search|                                                                               |
| WHOOGLE_VERSION                | No        | latest         |  YOLO                                                                                 |
| WHOOGLE_RESTART_TRIES          | No        | 5              |  How many times to attempt restart                                                    |
| WHOOGLE_CONFIG_LANGUAGE        | No        | en             |                                                                               |
| WHOOGLE_CONFIG_SEARCH_LANGUAGE | No        | en             |                                                                               |
| WHOOGLE_CONFIG_THEME           | No        | dark           |                                                                               |
| WHOOGLE_CONFIG_ALTS            | No        | true           |                                                                               |
| WHOOGLE_CONFIG_VIEW_IMAGE      | No        | true           |                                                                               |
| WHOOGLE_CONFIG_STYLE           | No        | -              | css config                                                                    |
| WHOOGLE_CONFIG_DISABLE         | No        | 1              | Disable customization                                                         |
| WHOOGLE_CONFIG_COUNTRY         | No        | US             |                                                                               |
| WHOOGLE_TOR_SERVICE            | No        | 0              | TOR disabled (mostly because rate limiting)                                   |
| WHOOGLE_CONFIG_TOR             | No        | 0              | TOR disabled (mostly because rate limiting)                                   |
|                                |           |                |                                                                               |





