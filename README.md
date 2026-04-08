# Pittsburghese Web

Tiny static web app for the Pittsburghese translator.

This repo is meant to be deployed behind your central Traefik instance.
It serves a single static frontend and lets the user's browser download the model from Hugging Face Hub.

## What this repo contains

- `public/index.html` – the app UI
- `public/config.js` – small config file with the Hugging Face model ID
- `Dockerfile` – tiny nginx static image
- `docker-compose.yml` – Traefik-ready service definition
- `.env.example` – set your domain

## Deployment flow

1. Push the model repo to Hugging Face
2. Set the final model ID in `public/config.js`
3. Copy `.env.example` to `.env` and set `DOMAIN=...`
4. Run `docker compose up -d`
5. Make sure the container joins the external `traefik-net` network used by your central proxy

## Notes

- The model is **not** baked into the container
- The browser downloads the ONNX files from Hugging Face, then caches them locally
- Your droplet only serves the tiny frontend shell
