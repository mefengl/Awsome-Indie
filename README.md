# Awsome-Indie
Simple tools enable a simple person to make a difference.

## Backend

### localhost

Always host on local computer first (maybe forever), because it's much easier to debug `locally`.

### json-server

json as DB, because... well, it's nice for 12 year old kid, and even better for me.

```bash
# Install DB
npm install -g json-server
# Make DB
echo '{"dbName": ["id":1,"msg":"hello world!"]}' >> db.json
# Run DB
json-server db.json --port:6661
# GET
curl http://localhost:6661/dbName
# POST
# if you use httpie, it will be easier
# and it's also have desktop application, make it much easier when you test `locally`
curl -d "id=2&msg='hi" -X POST http://localhost:6661/dbName
```
it also have `sort`, `limit` etc. option, see https://github.com/typicode/json-server

### Caddy

Connect the `https://<yoursite>.com` with `localhost:<port>`, hard to believe it can apply for SSL certificate automatically, like magic.

```bash
# here is homebrew, yes, `locally`, if you use ubuntu,centos... it will be apt-get, dnf, yum...
brew install caddy

# now the World Wide Web have such a honor to get access to you json DB
caddy reverse-proxy --from <yoursite>.com --to :6661
```

More: https://caddyserver.com/docs/quick-starts/reverse-proxy

### pm2

Caddy is already a system service, so won't shut down when log out. But json-server needs pm2.

```bash
# may need prefix 
npm install -g pm2
# pm2 run json-server, first `--` means pass through follow option to json-server rather than pm2
pm2 start json-server -- db.json --port 6661
```
