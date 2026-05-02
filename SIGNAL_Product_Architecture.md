# Signal — Outcome-Optimized Social Platform (Working Product Architecture)

## 0) Executive Summary
Signal is a social platform designed to maximize **learning, meaningful connection, and value creation** while minimizing compulsive usage patterns and low-signal content. It replaces engagement loops with intent-driven sessions, finite feeds, credibility-aware ranking, and friction-based moderation.

---

## 1) Product Architecture

### 1.1 User Roles
- **New User**
  - Can read public content, post with stricter limits, join onboarding circles.
  - Lower initial distribution until baseline trust is established.
- **Verified Expert**
  - Identity and expertise verified through multi-factor checks (credentials + peer attestation).
  - Higher credibility prior within tagged domains only.
- **Moderator**
  - Handles content disputes, moderation queues, trust-graph abuse reviews.
  - Can apply contextual penalties with audit trail.
- **Admin**
  - Policy management, system tuning, risk controls, transparency reporting.

### 1.2 Identity Layers
1. **Public Identity** (professional profile)
   - Name, credentials, expertise tags, contributions portfolio.
2. **Private Circles** (trusted groups)
   - Invite-based spaces for deeper discussion and accountability.
3. **Controlled Anonymity** (topic-scoped)
   - Pseudonymous posting allowed only in defined domains and moderated queues.
   - Anti-abuse controls: rate caps, stricter friction prompts, stronger penalties.

### 1.3 Feed System (Intent-Based, Finite)
User chooses session intent before viewing feed:
- **Learn Mode**: prioritize educational depth and credible evidence.
- **Connect Mode**: prioritize known-trust graph and active conversations.
- **Explore Mode**: controlled discovery of adjacent topics and novel contributors.

#### Feed constraints
- No infinite scroll.
- Session unit = **20 cards max** or **15 minutes**, whichever first.
- “End-of-session” summary shown after completion.

#### Ranking factors (not engagement)
- **Relevance**: semantic match to user intent + declared goals.
- **Credibility**: author/domain credibility + evidence quality.
- **Intent fit**: content type and depth aligned with selected mode.
- **Diversity guardrails**: topic/source diversification to avoid tunnel effects.

### 1.4 Content Types + Structured Format
All posts must declare one type:
1. **Insight** (educational)
2. **Proof** (data/results)
3. **Story** (experience)
4. **Question** (discussion)

#### Required template fields by type
- **Insight**: claim, explanation, practical takeaway, source links.
- **Proof**: hypothesis, method, result, limitations, evidence.
- **Story**: context, decision, outcome, lesson learned.
- **Question**: context, what was tried, specific ask.

Structured posting enforces high-signal clarity and reduces low-effort noise.

---

## 2) Reputation System

### 2.1 Credibility Score (0–100)
**Inputs**
- Posting consistency (cadence + quality stability)
- Peer validation from credible peers (weighted)
- Expertise-tag alignment (domain-relevant accuracy)
- Evidence quality (citations, reproducibility signals)

**Outputs**
- Ranking weight in relevant domains
- Eligibility for wider distribution
- Access to expert prompts/features

Formula (example):
```
credibility = 0.30*consistency + 0.35*peer_validation + 0.25*expertise_fit + 0.10*evidence_quality
```

### 2.2 Contribution Index (Value Added / Value Consumed)
Measures net social value:
- Value Added: accepted answers, saved resources, meaningful comments, follow-up quality.
- Value Consumed: passive read-only behavior, low-context posting, unresolved repetitive asks.

Example:
```
contribution_index = (value_added_points - noise_penalties) / max(1, value_consumed_points)
```

Penalties include repetitive low-effort replies, rage-bait framing, or off-topic spam.

### 2.3 Trust Graph
Edges are weighted by meaningful interaction quality:
- Long-form replies > reactions
- Constructive disagreement > agreement-only echoing
- Repeated reciprocal value exchange increases trust weight

Trust influences visibility within Connect Mode and moderation confidence.

---

## 3) Anti-Toxicity Engine (Friction, not blanket censorship)

### 3.1 Pre-Post Friction
- **“Are you sure?” prompts** for flagged language patterns.
- **Tone rewrite suggestions** (neutralize contempt/hostility).
- **2-minute delay buffer** for high-risk posts; user can revise/cancel.

### 3.2 Behavioral Penalties
- Reduced distribution of repeated toxic patterns.
- Temporary posting cooldowns.
- Reputation decay for repeated policy violations.

### 3.3 Context-Aware Moderation
- **Public mode**: strictest civility and evidence standards.
- **Private circles**: strong civility, more tolerance for unfinished ideas.
- **Anonymous mode**: highest friction + stricter thresholds + tighter rate limits.

### 3.4 Human-in-the-loop
- Escalation queue for contested AI decisions.
- Moderator actions require reason codes.
- User-visible appeal path and decision logs.

---

## 4) UX/UI System

### 4.1 Interface Rules
- No infinite scroll
- No autoplay
- No red dopamine badges
- No visible likes/follower counts by default
- Calm UI: neutral colors, whitespace, progressive disclosure

### 4.2 Dashboard Layout
- Top: session intent selector (Learn / Connect / Explore)
- Middle: “Today’s objectives” (user-defined goals)
- Main: finite feed card stack with progress indicator (e.g., Card 7/20)
- Right rail: trusted circle updates + saved items + knowledge trails
- Bottom: session timer + optional mindful break prompt

### 4.3 Feed Wireframe (Text)
```
[Intent: Learn]   [Topic: Distributed Systems]   [Session: 09:22 left]
---------------------------------------------------------------
Card 7/20 | Type: Proof | Credibility: High | Read time: 3 min
Title: Why event-driven retries failed in production
Summary: ...
Evidence: 2 linked artifacts
Actions: [Save] [Respond] [Open Discussion]
---------------------------------------------------------------
Next up preview: Insight (2 min)
```

### 4.4 Profile System (non-vanity)
- Highlights: expertise map, top contributions, collaboration history.
- Hidden by default: raw follower/like counts.
- Visible impact metrics: questions answered, projects helped, learning paths created.

### 4.5 Session Summary Screen
At end of finite session:
- Time spent
- Topics covered
- Value gained (learning score, meaningful interactions)
- Suggested next action (reflect, connect, pause)

---

## 5) Monetization (Ethical)

### 5.1 Core model
- Low-cost subscription tiers (individual + team/education)
- No ad inventory, no behavioral ad targeting

### 5.2 Creator monetization
- Voluntary tipping
- Paid circles/communities
- Premium knowledge packs/courses

### 5.3 Governance rule
- Product metrics can never optimize for ad CTR or watch-time.
- Any revenue feature must pass a “well-being impact review.”

---

## 6) Tech Stack + MVP Build

### 6.1 Recommended stack
- **Web**: Next.js (React, TypeScript)
- **Mobile**: React Native (Expo)
- **Backend**: Node.js (NestJS) + GraphQL (Apollo)
- **DB**: PostgreSQL
- **Cache/queues**: Redis (cache + BullMQ jobs)
- **Search**: PostgreSQL FTS initially; optional OpenSearch later
- **Infra**: Docker + Kubernetes (future), Terraform, managed Postgres

### 6.2 Service architecture (text diagram)
```
[Web/Mobile]
    |
[GraphQL Gateway]
    |---- Auth Service
    |---- Feed Orchestrator
    |---- Reputation Service
    |---- Moderation Service (AI + Human Queue)
    |---- Billing Service
    |
[PostgreSQL] [Redis] [Object Storage]
```

### 6.3 MVP scope (12–16 weeks)
- Intent-based finite feed
- Structured posting + type classifier
- Baseline credibility + contribution scoring
- Friction moderation + basic toxicity model
- Session summary + subscriptions + tipping v1

### 6.4 Future scope
- Advanced trust-graph propagation
- Better explanation UX for ranking decisions
- Expert verification marketplace
- Team workspaces and cohort learning journeys

---

## 7) Database Schema (Sample)

### users
- id (uuid, pk)
- email (unique)
- password_hash
- role (enum: new_user, expert, moderator, admin)
- status (enum: active, suspended, deleted)
- created_at, updated_at

### profiles
- user_id (uuid, pk/fk users.id)
- display_name
- bio
- public_identity_json
- expertise_tags (text[])
- anonymity_eligible (bool)
- created_at, updated_at

### posts
- id (uuid, pk)
- author_id (fk users.id)
- mode_visibility (enum: public, private_circle, anonymous_topic)
- post_type (enum: insight, proof, story, question)
- title
- body
- structured_fields_json
- topic_tags (text[])
- credibility_required (bool)
- published_at
- created_at, updated_at

### reputation_scores
- user_id (pk/fk users.id)
- credibility_score (numeric)
- contribution_index (numeric)
- toxicity_risk_score (numeric)
- last_recomputed_at

### interactions
- id (uuid, pk)
- actor_id (fk users.id)
- target_post_id (fk posts.id)
- interaction_type (enum: meaningful_comment, save, endorse_expertise, passive_view, report)
- quality_score (numeric)
- created_at

### trust_graph_edges
- source_user_id (fk users.id)
- target_user_id (fk users.id)
- trust_weight (numeric)
- basis_signals_json
- updated_at
- composite pk (source_user_id, target_user_id)

### moderation_events
- id (uuid, pk)
- user_id (fk users.id)
- post_id (nullable fk posts.id)
- event_type (enum: prompt, delayed_post, visibility_reduction, cooldown, strike)
- reason_code
- model_score (numeric)
- moderator_id (nullable fk users.id)
- created_at

---

## 8) API Examples (GraphQL)

### Query finite feed
```graphql
query Feed($intent: FeedIntent!, $cursor: String) {
  feed(intent: $intent, cursor: $cursor, limit: 20) {
    sessionId
    cardsRemaining
    items {
      id
      postType
      title
      summary
      credibilityBand
      estimatedReadMin
    }
    nextCursor
  }
}
```

### Create structured post
```graphql
mutation CreatePost($input: CreatePostInput!) {
  createPost(input: $input) {
    id
    postType
    moderationState
    publishAt
  }
}
```

### End session summary
```graphql
query SessionSummary($sessionId: ID!) {
  sessionSummary(sessionId: $sessionId) {
    timeSpentSec
    learningScore
    meaningfulInteractions
    suggestedNextAction
  }
}
```

---

## 9) AI Model Usage Plan

### 9.1 Content classification
- Multi-label transformer classifies post as Insight/Proof/Story/Question.
- Confidence below threshold => ask user to confirm/edit label.

### 9.2 Toxicity detection
- Ensemble model:
  - lexical toxicity detector
  - contextual harassment detector
  - conversation trajectory risk estimator
- Output drives friction actions, not auto-deletion by default.

### 9.3 Feed ranking (non-engagement)
Inputs:
- intent similarity
- credibility score
- trust proximity
- novelty/diversity constraints
- quality priors from structured completeness

Pseudo-code:
```python
def rank_posts(user, intent, candidates):
    scored = []
    for p in candidates:
        s_intent = sim(intent.embedding, p.embedding)
        s_cred = domain_credibility(p.author, intent.topic)
        s_trust = trust_weight(user.id, p.author_id)
        s_quality = structure_quality(p)
        s_diversity = diversity_bonus(user.recent_topics, p.topic)
        s_toxic_penalty = toxicity_risk_penalty(p)

        score = (
            0.35*s_intent +
            0.25*s_cred +
            0.15*s_trust +
            0.15*s_quality +
            0.10*s_diversity -
            s_toxic_penalty
        )
        scored.append((p, score))

    ranked = sorted(scored, key=lambda x: x[1], reverse=True)
    return finite_pack(ranked, max_items=20)
```

---

## 10) Launch Strategy

1. Start niche-first: e.g., **software developers**.
2. Invite-only onboarding with explicit norms.
3. Seed high-quality initial corpus (expert AMAs, curated explainers).
4. Strict early moderation and fast feedback loops.
5. Weekly transparency reports on moderation and ranking behavior.

---

## 11) Failure Analysis & Mitigations

### Risk 1: Engagement loops reappear
- **Mitigation**: enforce finite sessions platform-wide; governance checks for feature drift.

### Risk 2: Low-quality content flooding
- **Mitigation**: structured posting, early credibility gating, rate limits, contribution-based distribution.

### Risk 3: Monetization corrupts incentives
- **Mitigation**: subscriptions + creator payments only; explicit ban on ad-based optimization.

### Risk 4: User drop-off due to unfamiliar UX
- **Mitigation**: onboarding education, progressive feature unlock, visible personal outcome metrics.

### Risk 5: Over-moderation perception
- **Mitigation**: friction-first policy, transparent appeals, explainable model decisions.

---

## 12) MVP vs Future Feature Breakdown

### MVP
- Finite intent feed
- Structured content types
- Basic credibility + contribution scoring
- Friction moderation
- Session summaries
- Subscription + tipping

### Future
- Advanced trust graph propagation
- Multi-modal evidence verification
- Reputation portability/export
- Institutional communities and credential pathways

---

## 13) Example User Journey

**Persona**: Maya, junior backend engineer.
1. Onboards by selecting goals: “Learn distributed systems”, “Find mentors”.
2. Opens Learn Mode; receives 20-card session pack.
3. Saves two Proof posts, asks one structured Question.
4. Toxic phrasing warning appears once; edits post before publish.
5. Receives 3 meaningful replies from trusted circle.
6. Session summary: 14 minutes, learning score 82/100, 2 new trusted connections.
7. Returns next day with suggested path: “Retry semantics in queues.”

---

## 14) Brand Direction (Optional)
- **Tone**: calm, rigorous, constructive.
- **Color system**: slate + teal + soft amber accents (non-alerting).
- **Typography**: Inter / Source Sans for body, IBM Plex Serif for long-form readability.
- **Voice**: “helpful expert peer,” not viral entertainer.
