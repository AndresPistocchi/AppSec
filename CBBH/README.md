## cURL (Client URL)

| Command | Description |
|--------|------------|
| `curl -O` | Download a page or file and save output to disk |
| `curl -u user:pass` | Authenticate using username and password |
| `curl -h` | Display available cURL options |
| `curl -k` | Skip SSL certificate verification |
| `curl -v` | Show full HTTP request and response |
| `curl -vvv` | Extremely verbose HTTP output |

## cURL Examples

| Command | Description |
|--------|------------|
| `curl -X POST -d '{"search":"flag"}' -b 'PHPSESSID=<cookie>' -H 'Content-Type: application/json' http://target:port/query.php` | POST request with JSON body and session cookie |
| `curl -u username:password http://target:port/query.php?name=flag` | GET request using basic authentication |

## CRUD API

| Operation | HTTP Method |
|----------|-------------|
| Create | `POST` |
| Read | `GET` |
| Update | `PUT` |
| Delete | `DELETE` |

## CRUD API Examples

| Command | Description |
|--------|------------|
| `curl -X PUT http://target:port/api.php/city/Boston -d '{"city_name":"flag"}' -H 'Content-Type: application/json'` | Update resource |
| `curl -X DELETE http://target:port/api.php/city/anycity` | Delete resource |
| `curl -X GET http://target:port/api.php/city/flag` | Read resource |

## NSLOOKUP

| Command | Description |
|--------|------------|
| `nslookup example.com` | Resolve domain to IP |
| `nslookup -type=A example.com` | Retrieve A record |
| `nslookup -type=NS example.com` | Retrieve NS records |

## DIG

| Command | Description |
|--------|------------|
| `dig example.com` | Query DNS records |
| `dig A example.com` | Retrieve A record |
| `dig AAAA example.com` | Retrieve IPv6 record |
| `dig MX example.com` | Retrieve mail servers |
| `dig AXFR @targetIP example.com` | Attempt DNS zone transfer |

## DNSEnum

| Command | Description |
|--------|------------|
| `dnsenum --enum inlanefreight.com -f /usr/share/seclists/Discovery/DNS/subdomains-top1million-20000.txt` | Enumerate subdomains |

## GoBuster

| Command | Description |
|--------|------------|
| `gobuster vhost -u http://targetIP:port -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-110000.txt --append-domain example.com` | Virtual host brute-force |

## Certificate Transparency Logs

| Command | Description |
|--------|------------|
| `curl -s "https://crt.sh/?q=facebook.com&output=json" \| jq -r '.[] \| select(.name_value \| contains(\"dev\")) \| .name_value' \| sort -u` | Enumerate dev subdomains from CT logs |
