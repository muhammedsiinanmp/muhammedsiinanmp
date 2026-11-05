<img width="100%" src="https://capsule-render.vercel.app/api?type=waving&color=0:0f172a,50:1e3a8a,100:2343d6&height=200&section=header&text=Muhammed%20Sinan&fontSize=52&fontColor=ffffff&fontAlignY=36&desc=Python%20backend%20engineer%20%C2%B7%20AI%20developer%20tools&descAlignY=58&descSize=17&animation=fadeIn" alt="Muhammed Sinan, Python backend engineer building AI developer tools" />

<p align="center">
  <img src="https://readme-typing-svg.demolab.com?font=IBM+Plex+Mono&weight=500&size=18&pause=1200&color=2F6BFF&center=true&vCenter=true&width=640&lines=Django+%C2%B7+FastAPI+%C2%B7+Celery+%C2%B7+Postgres+%C2%B7+Redis;LangGraph+agents+that+review+pull+requests;Webhooks+%E2%86%92+queues+%E2%86%92+LLMs+%E2%86%92+inline+comments;Tests+first.+Trade-offs+written+down." alt="Django, FastAPI, Celery, Postgres, Redis. LangGraph agents that review pull requests." />
</p>

<p align="center">
  <a href="https://linkedin.com/in/muhammedsiinanmp"><img src="https://img.shields.io/badge/LinkedIn-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white" alt="LinkedIn" /></a>
  <a href="mailto:muhammedsiinanmp@gmail.com"><img src="https://img.shields.io/badge/muhammedsiinanmp@gmail.com-1e293b?style=for-the-badge&logo=gmail&logoColor=white" alt="Email" /></a>
  <img src="https://img.shields.io/badge/Kozhikode,_Kerala-1e293b?style=for-the-badge&logo=googlemaps&logoColor=white" alt="Kozhikode, Kerala" />
  <img src="https://img.shields.io/badge/Open_to-Backend_%26_AI_roles-2ea043?style=for-the-badge" alt="Open to backend and AI roles" />
</p>

<br />

I build **Python backends** with Django, FastAPI, Postgres, Redis and Celery, and I've been building **tools that review and check AI-written code**.
I write tests before features, record design trade-offs, and give every README a *Known limitations* section.

<br />

## 🧠 DevMind: AI pull-request reviewer

<p>
  <a href="https://github.com/muhammedsiinanmp/Devmind"><img src="https://img.shields.io/badge/source-Devmind-181717?style=flat-square&logo=github" alt="Source" /></a>
  <a href="https://github.com/muhammedsiinanmp/Devmind/actions/workflows/ci.yml"><img src="https://github.com/muhammedsiinanmp/Devmind/actions/workflows/ci.yml/badge.svg" alt="CI" /></a>
  <img src="https://img.shields.io/badge/tests-420_passing-2ea043?style=flat-square" alt="420 tests passing" />
  <img src="https://img.shields.io/badge/coverage-80%25%2B-2ea043?style=flat-square" alt="Coverage 80%+" />
  <img src="https://img.shields.io/badge/license-MIT-64748b?style=flat-square" alt="MIT" />
</p>

Open a pull request and DevMind reads the diff, reviews it for **security, quality and test coverage** in parallel, scores the risk from 0 to 100, and posts the findings back as **inline review comments**.

```mermaid
flowchart LR
    PR(["Pull request<br/>opened / updated"]) -->|HMAC-signed webhook| DJ["Django API"]
    DJ -->|enqueue| Q[("Redis")]
    Q --> W["Celery worker"]
    W -->|diff| AI["FastAPI<br/>LangGraph agent"]
    AI <-->|similar code| V[("Postgres<br/>+ pgvector")]
    AI -->|failover| LLM["Your keys → Gemini<br/>→ Groq → GitHub Models"]
    W -->|inline comments| GH(["GitHub review"])
```

<table>
<tr>
<td width="50%" valign="top">

**🕸️ 7-node LangGraph agent**<br/>
Three analyzers run as parallel branches, then results are de-duplicated and sorted by severity. A low-confidence review loops back, up to 3 passes.

**🔁 LLM failover**<br/>
Your own API keys first, then Gemini, Groq and GitHub Models. One Redis rate limit is shared by every worker.

</td>
<td width="50%" valign="top">

**🔐 Security**<br/>
Webhook signatures are checked before parsing. OAuth tokens and API keys are encrypted at rest. User-supplied URLs can't reach private IPs (SSRF guard).

**📈 Built to operate**<br/>
9 services in Docker Compose. Prometheus metrics, a provisioned Grafana dashboard, and CI that runs pytest against real Postgres and Redis.

</td>
</tr>
</table>

<p>
  <img src="https://skillicons.dev/icons?i=django,fastapi,py,postgres,redis,docker,nginx,prometheus,grafana,react,ts,tailwind&perline=12" alt="Django, FastAPI, Python, Postgres, Redis, Docker, Nginx, Prometheus, Grafana, React, TypeScript, Tailwind" />
</p>

<br />

## 👟 SneakIn: full-stack sneaker store

<p>
  <a href="https://github.com/muhammedsiinanmp/Sneak-in-ecommerce"><img src="https://img.shields.io/badge/source-Sneak--in--ecommerce-181717?style=flat-square&logo=github" alt="Source" /></a>
  <a href="https://github.com/muhammedsiinanmp/Sneak-in-ecommerce/actions/workflows/ci.yml"><img src="https://github.com/muhammedsiinanmp/Sneak-in-ecommerce/actions/workflows/ci.yml/badge.svg" alt="CI" /></a>
  <img src="https://img.shields.io/badge/deploy-GitHub_Actions_→_EC2-f59e0b?style=flat-square&logo=amazonaws&logoColor=white" alt="Deploys to EC2" />
</p>

A store with catalog filters, cart, wishlist, orders and an admin dashboard. Admins get an automated **daily sales report** from Celery Beat.

<table>
<tr>
<td align="center"><img src="https://raw.githubusercontent.com/muhammedsiinanmp/Sneak-in-ecommerce/main/docs/screenshots/home.jpg" alt="SneakIn home page" /><br/><sub>Home</sub></td>
<td align="center"><img src="https://raw.githubusercontent.com/muhammedsiinanmp/Sneak-in-ecommerce/main/docs/screenshots/collection.jpg" alt="Collection page with filters" /><br/><sub>Collection</sub></td>
<td align="center"><img src="https://raw.githubusercontent.com/muhammedsiinanmp/Sneak-in-ecommerce/main/docs/screenshots/product.jpg" alt="Product page" /><br/><sub>Product</sub></td>
</tr>
</table>

- 🔒 **No overselling.** Placing or cancelling an order locks the product rows, so two buyers can't take the last pair.
- 🪪 **JWT with rotation and blacklisting.** Every API view requires login unless it's explicitly public.
- 🧭 **Planning the move to services.** I wrote an [architecture analysis](https://github.com/muhammedsiinanmp/Sneak-in-ecommerce/tree/architecture/microservices-migration) using the strangler-fig pattern. It recommends 4 deployables and a worker, not one service per app, to avoid a distributed monolith.
- 🚀 **Shipped.** Nginx, Gunicorn, Postgres, Redis, Celery and Flower run in Docker Compose. GitHub Actions deploys to AWS EC2.

<p>
  <img src="https://skillicons.dev/icons?i=django,py,react,tailwind,postgres,redis,docker,nginx,githubactions,aws&perline=10" alt="Django, Python, React, Tailwind, Postgres, Redis, Docker, Nginx, GitHub Actions, AWS" />
</p>

<br />

## 🏭 Currently building

> [!NOTE]
> **[OpenFactory](https://github.com/muhammedsiinanmp/openfactory)** is an early-stage, spec-driven control plane for AI coding agents. Requirements become a task DAG, and each task runs in its own git worktree. Tests decide what passes, and every commit traces back to a requirement. *Phase 1 is in progress.*

<br />

## 🧩 More work

| | Project | What it is |
|:-:|---|---|
| 🎓 | [**Edustream**](https://github.com/muhammedsiinanmp/Edustream) | Course enrollment with an approval workflow. Students request courses and a principal approves them. Django · PostgreSQL · 172 tests |
| 🤝 | [**oss-contributor-agent**](https://github.com/muhammedsiinanmp/oss-contributor-agent) | Agents find open-source issues and draft fixes. A human approves every plan, diff and push |
| 💼 | [**Zignature**](https://github.com/mohmdsaalim/zignature-semantics) | Team job-agency platform. I set up the Django scaffold, user model, Docker + Nginx stack and OpenAPI docs |
| 📐 | [**system-design-mastery**](https://github.com/muhammedsiinanmp/system-design-mastery) | 33 topics so far, each covering how a system works, where it breaks, and the trade-offs, with sources cited |
| 🧮 | [**Leetcode**](https://github.com/muhammedsiinanmp/Leetcode) | Python solutions by topic, each with its approach and complexity, plus a repo-wide test script |

<br />

## 🛠️ Toolbox

<p align="center">
  <img src="https://skillicons.dev/icons?i=py,django,fastapi,postgres,redis,docker,nginx,githubactions,aws&perline=9" alt="Backend tools" /><br/>
  <img src="https://skillicons.dev/icons?i=grafana,prometheus,react,ts,vite,tailwind,git,linux,go&perline=9" alt="Ops, frontend and learning" />
</p>

<p align="center"><sub>Also: Celery · LangGraph · pgvector · pytest · uv · Claude Code. &nbsp;Learning Go (not production-level yet).</sub></p>

<br />

<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="https://streak-stats.demolab.com?user=muhammedsiinanmp&theme=tokyonight&hide_border=true&background=0D1117" />
    <img src="https://streak-stats.demolab.com?user=muhammedsiinanmp&hide_border=true" alt="GitHub contribution streak" />
  </picture>
</p>

<img width="100%" src="https://capsule-render.vercel.app/api?type=waving&color=0:2343d6,50:1e3a8a,100:0f172a&height=110&section=footer" alt="" />
