# The Agent Toolbox — Full Stack Inventory

---

## Search & web data
| Tool | What it does | Used by | Cost |
|---|---|---|---|
| **Serper** (serper.dev) | Google search results (SERPs) via API; 30-day disk cache | conference, outreach-agent | paid |
| **Tavily** | AI-oriented search API | conference | paid (free tier) |

## Fetch & scraping — the tiered "different curl" ladder
| Tool | What it does | Used by | Cost |
|---|---|---|---|
| **curl_cffi / curl-impersonate** | The "different curl" — HTTP client that **impersonates browser TLS fingerprints** to pass bot walls. Tier-1 fetch. | conference, outreach-agent | free (lib) |
| **Playwright** (headed/stealth, off-screen Chrome) | Browser automation; tier-2 fetch; passes DataDome/Cloudflare | capponi, conference, general-purpose, gustave, outreach-agent, seo-agent | free |
| **Puppeteer** | Headless Chrome automation | seo-agent | free |
| **Firecrawl** | Managed scrape/crawl API; tier-3 **last resort** (credits; OFF by default in conference) | conference, general-purpose, outreach-agent | paid |
| **trafilatura / readability / beautifulsoup4 / lxml** | HTML → clean text extraction | conference, seo-agent, mcp-google-ads, others | free |

## Contact & email enrichment
| Tool | What it does | Used by | Cost |
|---|---|---|---|
| **Tomba** | **Verified** email finder — the live/keeper provider | conference, outreach-agent | paid |
| **Dropcontact** | Email finder (pattern guesses) — **de-defaulted**, guesses blocked *(likely the "terrible, I'm switching" one from the episode)* | conference, outreach-agent | paid |
| **Hunter.io** | Email finder/verifier | conference, outreach-agent | paid |
| **contact-goat** (`pp-contact-goat` CLI) | LinkedIn search + warm-intro mapping + enrichment **waterfall** across sources | capponi, conference, kaREn | mixed |
| **Happenstance** | Warm-intro / network-path mapping | conference | free quota + paid |
| **Deepline** | Paid contact enrichment | conference | paid |

## LinkedIn & outreach channels
| Tool | What it does | Used by | Cost |
|---|---|---|---|
| **HeyReach** | LinkedIn outreach (the system can't go on LinkedIn directly) | conference, outreach-agent | paid |
| **linkedin-mcp** (stickerdaniel) | LinkedIn search via your own session | conference | free |

## LLM providers & routing
| Tool | What it does | Used by | Cost |
|---|---|---|---|
| **Anthropic / Claude Code** | The substrate; `claude -p` for agent-to-agent + the draft/judge path | all | sub |
| **OpenRouter** | Cheap models behind one OpenAI-compatible key (qwen categorizer, weekend research) | conference, outreach-agent | paid |
| **Local LLM** (LM-Studio-style, on-LAN) | Semantic voice-lint, on-LAN/free | conference | free |

## Google Workspace
| Tool | What it does | Used by | Cost |
|---|---|---|---|
| **gws CLI** (google-workspace, file keyring) | Gmail / Sheets / Drive / Calendar — read truth, gated writes, no MCP for the pipeline | conference, gustave, kaREn, outreach-agent | free (OAuth) |
| **WordLift** (MCP) | Knowledge-graph / SEO | seo-agent | sub |
| **mcp-google-ads** | Google Ads + analytics agent (also pulls in apify-style fetch, imap, ffmpeg, whisper, bs4) | mcp-google-ads | — |
| libs: **google-auth / google-auth-oauthlib / gspread** | Sheets/Gmail auth + access | several | free |

## Travel (gustave)
| Tool | What it does | Cost |
|---|---|---|
| **Airbnb MCP** (`@openbnb/mcp-server-airbnb`) | Stays search | free |
| **cheap-flights MCP** | Flight search (remote MCP) | free/test |
| **Duffel** (`duffel-flights` MCP + API) | Flights booking/search | paid |

## Media, transcripts & docs
| Tool | What it does | Used by | Cost |
|---|---|---|---|
| **yt-dlp** | YouTube video/transcript download | conference, gary-zee, gustave, outreach-agent, seo-agent | free |
| **ffmpeg** | Audio/video processing | mcp-google-ads, seo-agent | free |
| **whisper** | Speech-to-text (ASR) | mcp-google-ads, seo-agent | free/local |
| **Fathom / Grain** | Meeting recorders → call transcripts | meeting-importer, seo-agent, mcp-google-ads | sub |
| **pandoc** | Document format conversion | capponi | free |
| **reportlab / pillow / matplotlib** | PDF / image / chart generation | several | free |

## Messaging, orchestration & data
| Tool | What it does | Used by | Cost |
|---|---|---|---|
| **Telegram bot** | Orchestrator chat interface (Claudio) | abbado | free |
| **MCP** (Model Context Protocol) | Standard for connecting agents ↔ external systems | network-wide | free |
| **SQLite** | Local pipeline state / mirrors | abbado, conference, meeting-importer, outreach-agent, mcp-google-ads | free |
| libs: **pandas, validators, python-dotenv, requests, urllib3** | Plumbing | network-wide | free |

---

## "Little tools worth sharing" — the highlights for other builders
The non-obvious ones that punch above their weight:
1. **curl_cffi / curl-impersonate** — the cheap way past bot walls before you ever pay for Firecrawl.
2. **A tiered fetch ladder** (curl_cffi → stealth Playwright → Firecrawl last) so you spend credits only when free tiers fail.
3. **OpenRouter as a single key for "cheap model" jobs** (categorize/classify) while keeping Claude for drafting.
4. **gws CLI with a local file keyring** — Google Workspace from the terminal without MCP, the reason scheduled jobs must run in a local session.
5. **contact-goat** as a single front-end over a *waterfall* of contact sources (free → paid), so you only burn paid credits on the rows that survive the free steps.
6. **A local LLM on the LAN for the high-frequency cheap checks** (voice-lint) — zero marginal cost.
