# bm_ai_faq
Drupal 11 module for AI generated F.A.Q. content
Boom—leveled up and split into two clean modules:

1. **Enhanced FAQ generator (v2)**
   **Download:** [bm_ai_faq_v2.zip](sandbox:/mnt/data/bm_ai_faq_v2.zip)

What’s new:

* **Queue + Batch**: paste a big list → queued jobs via cron; “Dry run” previews via Batch API.
* **Multilingual**: set `langcode` per node (e.g., `nl`, `en`, `da`).
* **Moderation/Publishing**: choose publish state and optional `moderation_state`.
* **Field Mapping**: configure a specific taxonomy field (`taxonomy_field`) or auto-detect by vocabulary.
* **Body format**: pick the text format for `body`.
* **Title template**: use `{{question}}` plus optional prefix.
* **Update existing**: if a node with the same title exists, optionally update instead of creating duplicates.
* **Retries**: configurable `max_retries` for flaky provider calls.
* **Safer parsing**: resilient JSON extraction; still works if model returns fenced code.

Paths:

* Settings: `/admin/config/ai/faq`
* Generator: `/admin/content/ai/faq-generator`

2. **SERP discovery companion**
   **Download:** [bm_ai_faq_discovery.zip](sandbox:/mnt/data/bm_ai_faq_discovery.zip)

What it does:

* **Discovers trending questions** from search results (via **SerpAPI**; pluggable) using your **seed queries** or an ad-hoc query.
* Sends result snippets to your configured **LLM** to propose FAQ-style questions in JSON.
* **Review & select** suggested questions, then **queue** them to the generator (above) for answer creation + node creation.
* **Dedupes** against existing FAQ node titles.

Paths:

* Configure: `/admin/config/ai/faq-discovery`

  * Set SERP backend (SerpAPI key, market/language, max results)
  * Set AI provider/model and the extraction prompt
  * Add seed queries (one per line)
* Run: `/admin/content/ai/faq-discovery`

  * Optional ad-hoc query → discover → select → **Queue selected for generation**

Notes & next steps (optional polish)

* Add additional SERP plugins (Bing Web Search, Google Programmable Search) by extending `SerpClient`.
* Add a **cron** toggle in discovery to auto-run on a schedule (currently manual; easy to wire to cron).
* Add **source capture**: store the SERP result links used to propose each question in a field for auditability.
* Add **tone/brand presets** per language (prompt presets).
* Add **auto-tagging improvements**: call a second LLM step that maps discovered topics to your controlled vocabulary (synonym mapping).

