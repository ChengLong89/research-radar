# Instructions for each scheduled run

You are generating the weekly Research Radar digest in this repository. Use public sources only.

1. Read `config/topics.yaml` and `state/seen_papers.json`.
2. Search the sources listed in the config for items from the past 7 days (use web search and fetch;
   search each topic separately). Also check the release notes of each repo in `watch_repos`.
3. Drop anything whose URL or arXiv ID is already in `state/seen_papers.json`.
4. Score each remaining item 1–5 for relevance using the topic weights and `relevance_criteria`.
   Keep the top `max_items`.
5. Write `digests/YYYY-MM-DD.md` (today's date, in the configured language) with:
   - A 3-sentence "本周要点 / This week" summary at the top
   - For each item: title + link, source/date, relevance score, 2–3 sentence summary in your own words,
     and one line on "可借鉴之处 / What to borrow" for someone fine-tuning and optimizing enterprise agents
   - A short "框架更新 / Framework updates" section (only notable changes; omit if none)
   - If an item follows up earlier work already in `seen_papers.json`, say so and link the earlier digest
6. Every second run (when the latest file in `competitors/` is ≥ 13 days old or missing), also write
   `competitors/YYYY-MM-DD.md`: public enterprise/ERP AI announcements from the companies in `competitors`.
7. Append every new item to `state/seen_papers.json` as
   `{"id": "<arxiv id or url>", "title": "...", "date": "YYYY-MM-DD", "digest": "digests/YYYY-MM-DD.md", "topic": "..."}`.
8. Update the index between `<!-- INDEX:START -->` and `<!-- INDEX:END -->` in `README.md`
   (newest first, one line per digest with its 本周要点 headline).
9. Commit with message `digest: YYYY-MM-DD` and push to `main`.
10. Send a short notification summarizing the top 3 items with a link to the digest file on GitHub.

Rules: paraphrase — never copy abstracts or paragraphs; quote at most a short phrase. Never include
private, internal, or employer-confidential information. If a search fails, note it in the digest
rather than inventing content.
