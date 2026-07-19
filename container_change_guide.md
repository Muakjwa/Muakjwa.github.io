# CV 빌드 환경 세팅 (Ubuntu 22.04 컨테이너)

`tools/export-cv-pdf`로 `_tabs/about.md` → PDF를 뽑기 위한 환경 구성.
새 컨테이너에서 root로 아래 순서대로 실행.

## 0. 기본 도구

```bash
apt update
apt install -y wget curl git ca-certificates

apt remove -y chromium-browser 2>/dev/null || true

wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
apt install -y ./google-chrome-stable_current_amd64.deb
rm google-chrome-stable_current_amd64.deb


mv /usr/bin/google-chrome-stable /usr/bin/google-chrome-stable.real
cat > /usr/bin/google-chrome-stable << 'EOF'
#!/bin/bash
exec /usr/bin/google-chrome-stable.real --no-sandbox --disable-dev-shm-usage "$@"
EOF
chmod +x /usr/bin/google-chrome-stable

# 스크립트가 다른 이름으로 찾을 경우 대비
ln -sf /usr/bin/google-chrome-stable /usr/bin/google-chrome
ln -sf /usr/bin/google-chrome-stable /usr/bin/chromium-browser



apt install -y \
  fonts-liberation \
  fonts-dejavu-core \
  fonts-noto-core \
  fonts-noto-cjk \
  fonts-crosextra-carlito
fc-cache -fv



apt update && apt install -y gh

gh auth login        # GitHub.com → HTTPS → Yes → 브라우저(device flow)
gh auth setup-git
gh auth status