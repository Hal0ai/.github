<div align="center">

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="./brand/logo-halo-dark.svg">
  <img src="./brand/logo-halo-light.svg" alt="hal0" width="220">
</picture>

### Self-hosted home AI inference platform

Multi-backend, multi-slot, extensible. Built for AMD Strix Halo (iGPU + NPU).

[**hal0.dev**](https://hal0.dev) · [Install](https://hal0.dev/docs/install/) · [Docs](https://hal0.dev/docs/)

</div>

---

## What we're building

**hal0** is a polished, reliable inference platform for running LLMs at home — a one-command install for any modern Linux box, with model slots, an OpenAI-compatible API, a built-in dashboard, and a prewired chat UI.

It targets [**AMD "Strix Halo"** APUs](https://www.amd.com/en/products/processors/laptop/ryzen/ai-300-series.html) (Ryzen AI Max, gfx1151) but runs anywhere `llama.cpp`/`llama-server` runs. On Strix Halo, hal0 takes full advantage of the iGPU (ROCm + Vulkan) **and** the XDNA NPU via Foundry Local Manager — model swap, mixed-backend slots, and unified memory addressing all the way up to 124 GiB.

## Repos

| Repo | What it is |
| :--- | :--- |
| **[`hal0`](https://github.com/Hal0ai/hal0)** | The platform: orchestrator, slot lifecycle, dispatcher, dashboard, installer. Python (FastAPI) + Vue 3 + systemd. Apache-2.0. |
| **[`hal0-web`](https://github.com/Hal0ai/hal0-web)** | [hal0.dev](https://hal0.dev) — marketing site + Starlight docs. Astro + Tailwind v4. |
| **[`amd-strix-halo-toolboxes`](https://github.com/Hal0ai/amd-strix-halo-toolboxes)** | Friendly fork of [`kyuz0/amd-strix-halo-toolboxes`](https://github.com/kyuz0/amd-strix-halo-toolboxes) — adds `*-server` images (ENTRYPOINT=`llama-server`) so SlotManager can run them as systemd services. Published to GHCR at `ghcr.io/hal0ai/`. |

## Design tenets

- **One-shot install** — `curl … | bash` lands a working, idempotent stack. Re-running converges.
- **Slot lifecycle as a state machine** — every inference workload (chat, embed, rerank, STT, TTS, image) is a single-flight, systemd-managed unit with a known port and health probe.
- **Capability-first UX** — flat slots are real; the dashboard groups them into user-facing capabilities (Embed / Voice / Image / NPU rollup) so config stays legible.
- **Provider plurality** — `llama-server`, vLLM, Foundry Local Manager (XDNA NPU), moonshine (STT), kokoro/VibeVoice (TTS), Stable-Diffusion-WebUI all behind one OpenAI-compatible gateway.
- **No vendor lock-in** — Apache-2.0, open registry, OpenAI-compatible API surface. Bring your own models from HF.

## Status

v1.0 release candidate. Release pipeline (cosign keyless OIDC, signed tarball, `releases.hal0.dev` manifest) is wired end-to-end; first tag-push pending. See [`hal0/PLAN.md`](https://github.com/Hal0ai/hal0/blob/main/PLAN.md) for the live milestone view.

## Community & contact

- **Website** — [hal0.dev](https://hal0.dev)
- **Email** — `hello@hal0.dev`
- **Issues** — file in the relevant repo above
