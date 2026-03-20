# 🛡️ GigShield — AI-Powered Parametric Income Insurance for Delivery Partners

> *"When the rain stops orders, we make sure it doesn't stop their income."*

---

##  The Problem

India has over **15 million platform-based delivery partners** working with Zomato, Swiggy, Amazon, Zepto, and Blinkit. Their income is entirely dependent on being able to work outdoors — every day, every hour.

But external disruptions they cannot control — a sudden downpour, a flash flood, a local curfew — can wipe out **20–30% of their monthly earnings** in a single week. There is currently **no financial safety net** for this group.

They don't need health insurance. They don't need vehicle cover.  
They need **income protection** — fast, automatic, and affordable.

**GigShield** is that safety net.

---

##  Persona: Arjun, Swiggy Delivery Partner — Chennai

| Attribute | Detail |
|---|---|
| Name | Arjun Kumar |
| Age | 24 |
| Platform | Swiggy |
| City | Chennai |
| Operating Zones | Velachery, Saidapet, T. Nagar |
| Daily Working Hours | 7–9 hours |
| Average Daily Earnings | ₹850 |
| Typical Weekly Earnings | ₹5,100 – ₹5,950 |
| Vulnerability | Operates in historically flood-prone zones |

###  Arjun's Story

On a normal Wednesday, Arjun completes 18–22 deliveries. But when the Northeast Monsoon hits Chennai — which it does every October–December — his delivery zone near Velachery (known for waterlogging) becomes inaccessible. Orders dry up. He earns ₹200 on a day he should earn ₹850.

**That's a ₹650 loss in a single day. With no recourse.**

GigShield automatically detects the disruption using real-time weather data, cross-checks Arjun's GPS location, validates the income drop, and **credits ₹520 to his UPI account within minutes** — no forms, no calls, no waiting.

---

##  Application Workflow

```
  Worker Onboarding
        │
        ▼
  AI Risk Profiling  ←── Weather History + Zone Data + Delivery Activity
        │
        ▼
  Weekly Policy Activation  ←── Worker selects plan & pays weekly premium
        │
        ▼
  Real-Time Disruption Monitoring  ←── Weather API + AQI API + Traffic API
        │
        ▼
  Parametric Trigger Fired?  ──No──► Continue Monitoring
        │ Yes
        ▼
  AI Fraud Validation  ←── GPS Check + Activity Pattern + Weather Cross-Verify
        │
        ▼
  Claim Auto-Approved
        │
        ▼
  Instant Payout via UPI / Razorpay
        │
        ▼
  Worker Notified via App + WhatsApp
```

---

##  Weekly Premium Model

GigShield uses a **dynamic weekly pricing model** because gig workers operate and think week-to-week. Premiums are computed every Monday morning using AI risk scoring.

### How the Premium is Calculated

```
Weekly Premium = Base Rate × Zone Risk Multiplier × Weather Forecast Multiplier × Worker Tier Multiplier
```

| Factor | Description |
|---|---|
| Base Rate | ₹15 flat weekly base |
| Zone Risk Multiplier | 0.8x (Low) → 1.5x (High) based on historical flood/curfew data |
| Weather Forecast Multiplier | AI-adjusted based on next 7-day forecast from OpenWeatherMap |
| Worker Tier Multiplier | Loyalty discount for claim-free streaks (up to 0.85x after 4 clean weeks) |

### Illustrative Weekly Premium Examples

| Worker Zone | Risk Level | Weekly Premium | Weekly Coverage |
|---|---|---|---|
| Anna Nagar | Low | ₹15 | ₹1,500 |
| T. Nagar | Moderate | ₹20 | ₹2,000 |
| Velachery | High (flood-prone) | ₹27 | ₹2,700 |
| Saidapet | High | ₹25 | ₹2,500 |

Workers can also **upgrade their plan mid-week** if the AI predicts an incoming disruption — at a prorated additional cost.

---

##  Parametric Triggers

Parametric insurance pays out based on **objective data conditions**, not subjective claim reviews.

GigShield monitors a **Composite Disruption Score (CDS)** that combines multiple signals. A payout fires when CDS crosses the threshold — not just when one signal spikes.

### Trigger Conditions

| Trigger | Parameter | Threshold | Data Source |
|---|---|---|---|
| Heavy Rainfall | Rainfall (mm/hr) | > 35 mm/hr | OpenWeatherMap API |
| Flood Risk | Accumulated rainfall | > 100mm in 24 hrs | IMD / Weather API |
| Extreme Heat | Temperature | > 43°C | OpenWeatherMap API |
| Severe Pollution | AQI Index | > 300 | AQICN / AQI API |
| Curfew / Shutdown | Official govt alert | Area-level closure | News API / Mock |
| Delivery Order Drop | Platform order volume | Drop > 40% from baseline | Platform API / Mock |

### Composite Disruption Score (CDS)

```
CDS = w1(Rainfall_Score) + w2(Temp_Score) + w3(AQI_Score) + w4(Order_Drop_Score)
```

- CDS ≥ 0.6 → Partial Payout (50% of daily coverage)
- CDS ≥ 0.8 → Full Payout (100% of daily coverage)

This prevents single noisy signals from firing false claims.

---

##  AI / ML Integration

### 1. Zone Risk Scoring (Premium Calculation)

- **Model:** Gradient Boosting (XGBoost)
- **Input features:** Historical rainfall frequency, flood-zone classification, zone-level order drop patterns, AQI trends, past disruption events
- **Output:** Zone Risk Score (0.0 – 1.0) → maps to weekly premium
- **Training data:** IMD historical weather records (2015–2024), Chennai BBMP zone flood reports, mocked delivery volume data by zone
- **Retraining:** Weekly with updated weather and claim data
- **Hackathon fallback:** Pre-trained on synthetic Chennai zone data seeded with real monsoon patterns

### 2. Income Prediction & Loss Estimation

- **Model:** Time-Series Forecasting (LSTM / Prophet)
- **Input:** Worker's historical hourly earnings, day-of-week patterns, zone demand signals
- **Output:** Expected daily earnings → compared against actual earnings to calculate loss
- **Payout = min(Actual Loss, Coverage Cap) × CDS multiplier**
- **Hackathon fallback:** Rule-based baseline using registered avg. daily earnings when historical data is sparse

### 3. Fraud Detection

- **Model:** Isolation Forest (unsupervised anomaly detection)
- **Validates:**
  - GPS location during claimed disruption period
  - Movement patterns (was the worker actually stationary?)
  - Weather data vs claimed disruption (cross-validate)
  - Duplicate claims (same event, multiple submissions)
  - Historical fraud score of worker
- **Outcome:** Claim approved / flagged / rejected with confidence score

### 4. Predictive Pre-Coverage Alert

- 24–48 hrs before a likely disruption, the system proactively notifies the worker
- AI suggests temporary coverage upgrade
- Worker can accept with one tap → premium auto-deducted

---

##  Phase 1 — Market Crash Response: Adversarial Defense & Anti-Spoofing Strategy

> **The Attack:** 500 delivery partners. Fake GPS. Real payouts. A coordinated fraud ring organized on Telegram used GPS spoofing apps to falsely appear stranded in flood zones — draining the platform's liquidity pool. Simple GPS verification is dead. Here is how GigShield fights back.

GigShield's defense is built around **three core questions** the hackathon poses — answered with specific, layered logic:

---

###  Question 1: How Do You Spot the Faker from the Genuinely Stranded Worker?

**Answer: Behavioral DNA Fingerprinting**

Every enrolled worker builds a **personal activity baseline** over their first 2 weeks of active use:

| Signal | Genuine Worker Pattern | Fraud Ring Pattern |
|---|---|---|
| Pre-disruption activity | Was actively delivering 1–2 hrs before the event | Zero or minimal prior sessions |
| GPS movement before claim | Natural route polygon within their registered zone | Teleported to the zone right before claiming |
| Order attempt history | Shows attempted logins / failed order pickups | No app activity during the disruption window |
| Session age | 10+ sessions in the system | Account < 5 sessions old ("cold start") |
| GPS variance | Noisy, organic path with minor drift | Unnaturally static or perfectly rounded coordinates (hallmark of spoofed GPS) |

**The rule:** A claim is only eligible if the worker has **completed ≥ 5 verified delivery sessions** in the platform prior to the event. This makes fraud rings economically unviable — they must fake real delivery activity for days before they can even attempt a claim.

A genuine worker stranded by a flood shows a **recognizable signature**: active before the storm, GPS stopped inside their known zone, order drop-off aligns with weather data. A spoofer shows a **cold, clean, suspiciously perfect** GPS coordinate and no delivery history. The model detects this contrast with high confidence.

---

###  Question 2: What Data Catches a Coordinated Fraud Ring?

**Answer: Cross-Worker Cluster Anomaly Detection**

A single spoofed claim is hard to catch. But **500 simultaneous claims from the same 1km² grid cell** is statistically impossible in any real disruption.

GigShield runs a **real-time Cluster Fraud Score** on every batch of simultaneous claims:

```
Cluster Fraud Score = f(
  claims_per_km²  in the last 30 minutes,
  % of claimants with fewer than 5 prior delivery sessions,
  % of claimants registered within the last 7 days,
  std_deviation of GPS coordinates  [spoofed = unnaturally uniform / too tight],
  % of claimants sharing the same device fingerprint prefix or IP subnet
)
```

**Thresholds:**
- Cluster Fraud Score **> 0.75** → Entire claim batch auto-held for review
- **> 40% of claimants** share same device fingerprint prefix → Flagged as coordinated fraud
- **> 5 registrations** from same IP subnet within 1 hour → Account creation frozen

**Why this catches Telegram rings specifically:**
- Fraud rings recruit members who all register around the same time → triggers new-account clustering signal
- They share APK spoofing tools with similar fingerprint signatures → triggers device-prefix signal
- Real floods create **dispersed, noisy GPS clusters** across a zone. Coordinated spoofers create **unnaturally tight or grid-aligned coordinates** — statistically distinguishable from organic movement

**Multi-source weather corroboration (the ultimate truth layer):**

GPS spoofing cannot fake the weather. Every claim must be corroborated by **at least 2 independent external sources** before payout:

| Source | What It Confirms |
|---|---|
| OpenWeatherMap API | Rainfall intensity / temperature in the claimed zone |
| IMD (India Met Dept) real-time alerts | Official government weather advisory |
| Google Maps / Ola Maps disruption data | Reported road closures in the zone |
| News API | Local media mentions of the disruption event |

**No external corroboration = No payout.** A worker can be in the right GPS zone, at the right time, with a perfect claim — but if none of the above sources confirm an actual disruption event in that zone, the claim is rejected automatically. This single rule alone defeats most GPS spoofing attacks.

**Device & Account Hygiene:**

| Check | Implementation |
|---|---|
| Device Fingerprinting | One active policy per unique device fingerprint |
| SIM-based Identity | OTP verification ties each policy to a phone number — one policy per SIM |
| New Account Cooling Period | Claims blocked for the first 5 sessions — no Day-1 payouts |
| IP Subnet Rate Limiting | >5 registrations from the same IP range in 1 hour triggers a hold |

---

###  Question 3: How Do You Flag Bad Actors Without Punishing Honest Workers?

**Answer: Asymmetric Review — Hold First, Reject Only After Verification**

The worst outcome for GigShield is an honest worker getting wrongly denied during a real flood. Our fraud response is designed around **minimizing false positives** at all costs:

**When a claim is flagged (not outright rejected):**

```
Flagged Claim Flow:
  ├── Worker receives WhatsApp message within 2 minutes:
  │     "Your claim is under a quick verification check.
  │      You'll receive your payout within 2 hours."
  │
  ├── Lightweight manual review triggered (1 reviewer, 2-hour SLA)
  │     Reviewer checks ONE additional signal:
  │     - Public news confirmation of the disruption
  │     - Worker's pre-event delivery session history
  │     - Photo-on-demand (optional, only for repeat-flagged accounts)
  │
  ├── If GENUINE → Payout released immediately + apology message sent
  │
  └── If CONFIRMED FRAUD → Account suspended + flagged in shared fraud registry
```

**Graduated response — not binary:**

| Fraud Confidence Score | Action |
|---|---|
| < 0.4 (Low suspicion) | Auto-approved, no friction |
| 0.4 – 0.75 (Medium) | Auto-approved + silent flag added to worker profile for monitoring |
| 0.75 – 0.9 (High) | Claim held, human review within 2 hours, worker notified |
| > 0.9 (Near-certain fraud) | Claim rejected, worker notified with appeal option |

**The appeal mechanism:** Every rejected worker can submit a one-tap appeal with a photo or a government alert screenshot. This is the critical safety valve that ensures an honest worker caught by a false positive is **never permanently locked out** of their coverage.

The key principle: **We hold claims. We don't kill them.** A 2-hour delay for an honest worker is acceptable. A permanent denial is not.

---

## Market Crash Resilience — Liquidity Pool Protection

> **Scenario:** A catastrophic weather event (e.g., Chennai's 2015-scale floods) triggers simultaneous payouts for 80–90% of enrolled workers in a single week, risking insolvency of the liquidity pool.

GigShield is designed with a **three-layer financial resilience model** to survive black swan payout events:

### Layer 1 — Tiered Reserve Fund Structure

| Reserve Tier | Purpose | Size |
|---|---|---|
| Operational Reserve | Normal weekly payouts | 1.5× average weekly claim volume |
| Stress Reserve | High-disruption weeks (e.g., cyclone) | 3× average weekly claim volume |
| Emergency Reserve | Catastrophic event (>70% payout rate) | Reinsurance trigger threshold |

Premiums collected each week are allocated: **60% to Operational Reserve, 25% to Stress Reserve, 15% to platform fee + Emergency Reserve.**

### Layer 2 — Dynamic Payout Throttling

In a market crash scenario, GigShield does **not** pay 100% of claims instantly and drain the pool:

```
If (simultaneous_claims_this_hour / enrolled_workers) > 0.6:
    → Activate "Surge Mode"
    → Payout = min(CDS_payout, Surge_Payout_Cap)
    → Notify workers: "Disruption event detected. Payout processing within 4 hours."
```

- **Surge Mode** caps individual payouts at 60% of coverage, with the remaining 40% released within 48 hours as the reserve stabilizes.
- Workers are **informed proactively** via WhatsApp — they know they'll get paid, just in a guaranteed 2-stage release. This maintains trust without bankrupting the pool.

### Layer 3 — Reinsurance Trigger (Phase 3 Feature)

For production deployment, GigShield would integrate a **parametric reinsurance layer**: when cumulative weekly payouts exceed 2× the stress reserve threshold, a pre-negotiated reinsurance policy automatically kicks in to cover the excess. This is modeled after how catastrophe bonds work in traditional insurance.

For the hackathon, this is simulated as a mock reinsurance API that returns a coverage top-up amount when triggered.

### Financial Viability Snapshot

Assuming 1,000 enrolled workers in Chennai, average premium ₹20/week:

| Metric | Value |
|---|---|
| Weekly Premium Pool | ₹20,000 |
| Expected Normal Claim Rate | 15% of workers × avg ₹400 payout = ₹6,000 |
| Normal Week Loss Ratio | 30% — healthy |
| Stress Week (50% claim rate) | ₹20,000 payout — covered by Stress Reserve |
| Catastrophic Week (80% claim rate) | ₹32,000 — Stress Reserve + Emergency Reserve triggered |

At scale (10,000 workers), the reserve model becomes more stable due to **geographic diversification** — not all zones get hit simultaneously.

---

## 🖥️ Platform Choice: Web Application (Progressive Web App)

We chose a **Web Application (PWA)** for the following reasons:

- No app store friction — works on any smartphone browser
- Faster build cycle during hackathon phases
- Easy API integration and testing
- Can be accessed on low-end Android phones common among delivery workers
- Progressive enhancement — works even on slow connections

Future roadmap includes a native mobile app with offline support.

---

##  System Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                     GigShield Platform                       │
│                                                              │
│  ┌──────────────┐        ┌───────────────────────────────┐  │
│  │  Worker PWA  │◄──────►│       Backend API Server       │  │
│  │ (React.js)   │        │    (Node.js + Express.js)      │  │
│  └──────────────┘        └───────────┬───────────────────┘  │
│                                      │                       │
│              ┌───────────────────────┼────────────────────┐  │
│              │                       │                    │  │
│  ┌───────────▼──────┐  ┌────────────▼──────┐  ┌─────────▼─┐│
│  │  AI / ML Engine  │  │  Claims Engine     │  │  Policy   ││
│  │  (Python Flask)  │  │  (Parametric       │  │  Manager  ││
│  │                  │  │   Automation)      │  │           ││
│  │ - Risk Scoring   │  │                    │  │- Weekly   ││
│  │ - Income Model   │  │ - Trigger Monitor  │  │  Pricing  ││
│  │ - Fraud Detect   │  │ - Auto Claim Init  │  │- Coverage ││
│  │ - Pre-alerts     │  │ - Payout Process   │  │  Mgmt     ││
│  └──────────────────┘  └────────────────────┘  └───────────┘│
│                                      │                       │
│              ┌───────────────────────┼────────────────────┐  │
│              │                       │                    │  │
│  ┌───────────▼──────┐  ┌────────────▼──────┐  ┌─────────▼─┐│
│  │  External APIs   │  │    Database        │  │  Payment  ││
│  │                  │  │  (PostgreSQL)      │  │  Gateway  ││
│  │ - OpenWeather    │  │                    │  │           ││
│  │ - AQI API        │  │ - Workers          │  │ - Razorpay││
│  │ - Maps API       │  │ - Policies         │  │ - UPI     ││
│  │ - News/Alert API │  │ - Claims           │  │  Sandbox  ││
│  └──────────────────┘  └────────────────────┘  └───────────┘│
└─────────────────────────────────────────────────────────────┘
```

---

##  Technology Stack

| Layer | Technology |
|---|---|
| Frontend | React.js, Tailwind CSS, PWA |
| Backend | Node.js, Express.js |
| AI / ML | Python, Flask, Scikit-learn, XGBoost, Prophet |
| Database | PostgreSQL |
| Weather API | OpenWeatherMap (free tier) |
| Air Quality | AQICN API (free tier) |
| Maps / Location | Google Maps API |
| Payments | Razorpay Test Mode + UPI Simulator |
| Hosting | Render / Railway (free tier for hackathon) |
| Notifications | WhatsApp Business API (Twilio sandbox) |

---

##  Development Plan

### Phase 1 — Ideation & Foundation (March 4–20)
- [x] Define problem statement and persona (Arjun, Chennai)
- [x] Design full application workflow
- [x] Define parametric triggers and CDS model
- [x] Design weekly premium pricing logic
- [x] Define adversarial fraud defense strategy
- [x] Define liquidity pool resilience model
- [x] Set up GitHub repository
- [ ] Build basic UI screens (Registration, Dashboard, Policy)
- [ ] Connect OpenWeather API (mock responses)

### Phase 2 — Automation & Protection (March 21 – April 4)
- [ ] Worker registration and onboarding flow
- [ ] AI risk scoring engine (Zone Risk Model)
- [ ] Dynamic weekly premium calculator
- [ ] Parametric trigger engine (3–5 automated triggers)
- [ ] Basic claims automation
- [ ] Razorpay sandbox integration

### Phase 3 — Scale & Optimise (April 5–17)
- [ ] Advanced fraud detection: behavioral fingerprinting + cluster detection
- [ ] Income prediction model (LSTM)
- [ ] Surge Mode / dynamic payout throttling
- [ ] Worker dashboard (earnings protected, claim history)
- [ ] Admin dashboard (loss ratios, fraud alerts, zone risk heatmap)
- [ ] Predictive pre-coverage alert system
- [ ] Reinsurance trigger simulation
- [ ] Final demo preparation

---

##  Team

| Member | Role |
|---|---|
| Member 1 | Frontend (React PWA, Dashboards) |
| Member 2 | Backend (Node.js API, Claims Engine) |
| Member 3 | AI / ML (Risk Model, Fraud Detection, Income Model) |
| Member 4 | Integration (APIs, Payment Gateway, Notifications) |
| Member 5 | Product & Design (UX, Documentation, Demo) |

---

## 🔗 Links

- **Repository:** *https://github.com/Ranjita-haravi/GuideWire*
- **Demo Video:** *https://drive.google.com/drive/folders/12Y-3GRFXQMGGDxDBdjeKMny7eybgwYkr?usp=sharing*


---

## 📄 License

MIT License — built for Guidewire DEVTrails 2026 University Hackathon.
