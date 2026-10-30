# Wispbyte pe chalane ke steps (Docker nahi chahiye)

1. Wispbyte panel me **Python** server banao, saari files (zip extract karke) upload karo.
2. Startup / main file: `addon.py`   |   Requirements file: `requirements.txt`
   (agar panel me "extra packages" ka option hai to wahi list: requests curl_cffi beautifulsoup4 lxml Pillow)
3. Environment variables (Startup / Variables tab):
   - `DB_PATH` = `data.db`            (account/data isi folder me save hoga; disk persistent hai)
   - `PROTECT` = `log`  (pehle dry-run; sab theek chale to `on`)
   - `CF_TUNNEL_TOKEN` = <Cloudflare tunnel token>   (neeche dekho - domain/https ke liye)
4. Port ki chinta nahi: app khud panel ka `SERVER_PORT` use karti hai.
5. RAM: app container ki limit khud padh leti hai (512 MB pe ~330 MB par cache saaf karti hai).

## Cloudflare Tunnel (domain + https ke liye)
Wispbyte sirf IP:PORT deta hai, aur Cloudflare proxy random port pe nahi chalta.
Isliye: Cloudflare dashboard -> Zero Trust -> Networks -> Tunnels -> Create tunnel (Cloudflared)
-> token copy karo -> upar `CF_TUNNEL_TOKEN` me daalo.
Tunnel me Public hostname: apna domain, Service: `HTTP` `localhost:<SERVER_PORT>`
(panel me jo port dikhe wahi; port badle to tunnel ka service bhi badlo).
