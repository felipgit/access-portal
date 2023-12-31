# Selfhosted Access Portal
Based on Traefik as proxy and Authelia as the authentication middleware. It is expected to have port 80 and 443 exposed to this. All secrets/passwords should be changed with something like:
```bash
openssl rand -base64 48
```
# Installation
1. Download the repo
```bash
git clone git@github.com:felipgit/access-portal.git
```
2. Customize to your needs by changing the domain example.com to your own and other subdomains if you want to.  
_Recommendation: You can configure a sub domain (test.example.com, instead of example.com). For example set a DNS record to match *.test.myowndomain.com instead of example.com._  
- Change values in `docker-compse.yml`
- Change values in `authelia/configuration.yml`
- Optional: Customize stuff in `authelia/assets`

3. Start the stack:
```bash
docker-compose up -d
```
4. Give it 2 minutes to start all services and fetch certificates from lets encrypt.
# What now?
There are 3 preconfigured users wich you can use.
| Username | Password | Groups |
|---|---|---|
| john | password | admins, dev |
| james | password | sales |
| bob | password | dev |

If you need to do a password reset or configure 2FA device for a user, it will send an email. In this POC I have decided to only post the mail to an `email.txt` which will be located in `authelia` folder.
## Public
URL: https://public.example.com  
If you go to here you will get a simple whoami with some stats, no authentication required.
## Traefik Dashboard
URL: https://traefik.example.com  
Will require an authenticated user in the admins group.
## Authelia Portal
URL: https://auth.example.com  
Any user can get to the authentication portal and manage their credentials and auth devices.
## One Factor Authentication
URL: https://one.example.com  
A simple blue web page that requires group dev and one factor (username and password).
## Two Factor Authentication
URL: https://two.example.com  
A simple red web page that requires group sales and two factor (username and password + TOTP or a security key)
# What can be improved?
- Forward auth
- Add example with cloudflare for SSL
- Segregated networks
- Add SMTP example
