# schlangeweile

Self-hosted AI chat for Home Assistant — with arm64 support that actually
works on ARMv8.0 hardware (Hardkernel Odroid N2+, Raspberry Pi 4/5), where
plenty of prebuilt images die with `Illegal instruction`.

## Home Assistant add-ons

### AnythingLLM
One container, no external database: AI chat with a built-in document
pipeline (RAG), embedded SQLite + LanceDB, and native multi-user
administration. ~290 MiB RAM idle on amd64.

[![Open your Home Assistant instance and add the AnythingLLM repository.](https://my.home-assistant.io/badges/supervisor_add_addon_repository.svg)](https://my.home-assistant.io/redirect/supervisor_add_addon_repository/?repository_url=https%3A%2F%2Fgithub.com%2Fschlangeweile%2Fha-addon-anythingllm)

### LibreChat
The full chat platform: FerretDB/PostgreSQL document store, Meilisearch
full-text search and an admin panel — assembled from official multi-arch
release artifacts and supervised by s6-overlay.

[![Open your Home Assistant instance and add the LibreChat repository.](https://my.home-assistant.io/badges/supervisor_add_addon_repository.svg)](https://my.home-assistant.io/redirect/supervisor_add_addon_repository/?repository_url=https%3A%2F%2Fgithub.com%2Fschlangeweile%2Fha-addon-librechat)

## Why the ARMv8.0 focus

Official MongoDB arm64 builds require ARMv8.2 (LSE atomics) and crash with
`Illegal instruction` on an Odroid N2+. Every native binary these add-ons
ship is scanned for LSE opcodes and run under QEMU with `-cpu cortex-a53`
before release. The LibreChat add-on works around this with
FerretDB/DocumentDB; the AnythingLLM add-on avoids external services
entirely.

## Links

- [AnythingLLM add-on](https://github.com/schlangeweile/ha-addon-anythingllm) · [LibreChat add-on](https://github.com/schlangeweile/ha-addon-librechat)
- Upstream: [Mintplex Labs / AnythingLLM](https://github.com/Mintplex-Labs/anything-llm) (MIT) · [LibreChat](https://www.librechat.ai) (MIT)

---

Community projects, not affiliated with Mintplex Labs, LibreChat or Home
Assistant. Both add-ons are Apache-2.0.
