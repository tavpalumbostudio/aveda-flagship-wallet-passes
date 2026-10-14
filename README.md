# Aveda Flagship — Apple Wallet pass templates

Public asset bundle for **`aveda-flagship-api`** production servers.

These are **template images only** (no certificates or secrets).

## Server install (usvaavedaapp01)

```bash
cd /opt/aveda-api/tav/deploy/aveda-flagship-api/current

# clone or download this repo, then:
cp -R passes/* ./passes/
# or extract tarball into ./passes/

mkdir -p passes/transactions
chown -R avedaapp:avedaapp passes/

sudo /bin/su - avedaapp -c 'pm2 restart aveda-flagship-api'
```

## Verify

```bash
test -f passes/templatepass/logo.png && echo "passes OK"

curl -s http://localhost:5055/tecmark
curl -s -o /tmp/test.pkpass -w "HTTP %{http_code}\n" \
  "http://localhost:5055/tecmark/7171400000020000.pkpass"
file /tmp/test.pkpass
```

Expected: HTTP **200**, file type **Zip archive** (`.pkpass`).

## Layout

```
passes/
  templatepass/              # member card assets
  templatepasscertificate/   # certificate pass assets
  transactions/              # runtime temp dir (must exist, writable)
```
