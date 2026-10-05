# Demo "world-in-numbers" do OpenMontage

Vídeo: [`videos/world-in-numbers.mp4`](videos/world-in-numbers.mp4) — 1920x1080, 30 fps, ~23 s, 4,4 MB.
Feito sem nenhuma chave de API (só componentes do Remotion: textos, números e gráficos animados).

## Passos usados

```bash
git clone --depth 1 https://github.com/calesthio/OpenMontage.git
cd OpenMontage/remotion-composer
npm install
npx remotion render src/index.tsx Explainer ../projects/demos/renders/world-in-numbers.mp4 \
  --props public/demo-props/world-in-numbers.json --codec h264 \
  --browser-executable /opt/pw-browsers/chromium_headless_shell-1194/chrome-linux/headless_shell
```

Em um computador comum basta `./render-demo.sh world-in-numbers` dentro da pasta do OpenMontage.

## Problemas resolvidos (específicos da máquina na nuvem)

1. O Remotion tenta baixar o próprio navegador de `remotion.media`, que é bloqueado pela rede
   desta máquina. Solução: usar o Chromium já instalado (`--browser-executable`).
2. O navegador não carregava as fontes do Google (`ERR_CERT_AUTHORITY_INVALID`) porque não
   confiava nos certificados do proxy de rede da máquina. Solução: cadastrar esses certificados
   no repositório de confiança do Chromium com `certutil` (pacote `libnss3-tools`).
