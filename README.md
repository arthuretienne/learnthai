# 🇹🇭 Thai Training OS (learnthai)

Une plateforme d'entraînement au thaï qui **mesure ce que l'on sait réellement faire**, et pas simplement l'activité dans l'application.

> *Build a language-learning system that measures real ability rather than app activity.*

## Documents

| Document | Contenu |
|---|---|
| [`docs/VISION.md`](docs/VISION.md) | Product Vision & Master Brief (le « pourquoi » et le « quoi ») |
| [`docs/PRD.md`](docs/PRD.md) | PRD technique : architecture, modèle de données, APIs, algorithmes de scoring, parole, moteur adaptatif, contenu, métriques, tests d'honnêteté, plan du MVP |

## Statut

Phase de cadrage. Aucun code pour l'instant : la prochaine étape est la **semaine 1 de spikes** décrite au §16 du PRD (PWA iOS et micro, saisie thaïe, évaluation de prononciation `th-TH`, voix TTS, contours de ton, segmentation).

## Stack prévue (résumé)

Next.js (TypeScript, PWA) · PostgreSQL / Supabase · service Python FastAPI (PyThaiNLP, audio, tons) · Claude API (correction et génération de contenu) · Azure Speech `th-TH` · Cloudflare R2 pour l'audio.
