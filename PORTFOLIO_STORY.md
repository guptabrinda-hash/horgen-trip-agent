# Horgen Trip Recommender Agent — Portfolio Story

## 🎯 Executive Summary

I built an autonomous AI agent that doesn't just recommend family trips—it **actually executes them**. 

The agent:
- Searches for destinations autonomously
- Builds detailed 5-day itineraries
- Ranks options by budget and fit
- **Sends email confirmation** (Gmail integration)
- **Books calendar events** (Google Calendar integration)

This is **agent** (executes), not **chatbot** (recommends).

---

## 🔍 The Problem I Solved

My family needed to plan October 2026 trips with:
- Budget: CHF 1200-1500 for 5 days
- Driving: Max 5 hours from Horgen, Switzerland
- Activities: Hiking, lakes, child-friendly
- Dates: School holidays only (Oct 3-18, 2026)

A typical chatbot would say: "Here are 3 options. You book yourself."

I wanted an **agent** that says: "Here are 3 options. I'll book it for you."

---

## 💡 How It Works

### Phase 1: Specification
I wrote clear constraints for the agent:
- School holidays (Herbstferien Oct 3-18, 2026)
- Budget tier (CHF 1200-1500)
- Driving distance (max 5 hours)
- Family profile (2 adults, 6-year-old)

See: `screenshots/01_system_prompt_agent_instructions.png`

### Phase 2: Autonomous Planning
Claude autonomously:
1. Searched for 5+ family-friendly destinations
2. Evaluated each against constraints
3. Built 3 detailed 5-day itineraries with hotels, restaurants, activities
4. Ranked by value and fit

See: `screenshots/03-08_option_details_and_costs.png`

### Phase 3: Constraint Analysis
Each option was analyzed for:
- ✅ Budget adherence (CHF 1200-1500)
- ✅ Driving distance (max 5 hours)
- ✅ School holiday dates (Oct 3-18)
- ✅ Family-friendliness (age 6+)

Results:
- **Appenzell:** CHF 1,470 ✅ Within budget, 90 min drive
- **Lucerne:** CHF 1,505 ⚠️ Slightly over, 90 min drive
- **Interlaken:** CHF 1,715 ❌ Over budget, 3 hour drive

### Phase 4: Human Approval Gate
Agent stopped and asked: "Which destination would you prefer?"

**Why?** Because choosing a destination is a human value judgment. The algorithm can rank by metrics, but humans decide what they want.

I chose: **APPENZELL ALPS**

See: `screenshots/09-10_agent_requesting_user_choice.png`

### Phase 5: Autonomous Execution
Once approved, Claude **autonomously**:
1. Sent detailed email with complete itinerary (Gmail connector)
2. Created Google Calendar event for Oct 3-8, 2026 (Google Calendar connector)
3. Added location, activities, restaurant info to calendar
4. Reported: "Trip planned and booked!"

See: `screenshots/11-14_execution_and_proof.png`

---

## 🧠 Key Learnings (AI PM Insights)

### 1. Agent ≠ Chatbot

**What I observed:**
- Chatbot: "Here are your options. Go book yourself."
- Agent: "Here are your options. I'll book it." [Sends email + calendar]

"As an AI PM, I distinguish between recommendation engines and true agents. Agents need:
- Execution capabilities (connectors to email, calendar, APIs)
- Approval gates (safety checkpoints)
- Measurable outcomes (did it actually work?)"

### 2. Constraints Are Core Product Features

**What I observed:**
Claude automatically checked:
- School holidays (Oct 3-18, 2026) ✅
- Budget (CHF 1200-1500) ✅
- Driving distance (max 5 hours) ✅

Any destination violating constraints ranked lower.

"Constraints aren't restrictions—they're the product. They encode what matters to users. Budget matters. Distance matters. Family-friendliness matters. These shape the ranking algorithm and prevent bad recommendations."

### 3. Measure Real Outcomes, Not Text Output

**What I observed:**
The email arrived. The calendar event appeared.

"Success metrics aren't 'did it output text?' They're 'did it complete the task?' In production: Did the email actually deliver? Did the calendar event actually create? Did the booking actually go through? That's how you measure agent success."

### 4. Strategic Autonomy Requires Approval Gates

**What I observed:**
Claude autonomously searched, planned, ranked. But it **stopped** before executing to ask which destination I wanted.

**Why?** Because choosing a destination requires human judgment.

"True autonomy isn't 'no human input.' It's strategic autonomy with intelligent checkpoints. Automate decisions the AI makes well (search, rank, evaluate). Ask humans for decisions requiring judgment (which option?). This builds trust."

### 5. Prompt Efficiency Matters

**What I observed:**
I initially thought I needed 2 messages (system prompt + user request). Claude executed after the first message alone. The second was redundant.

"A well-structured prompt with clear intent triggers autonomous execution without follow-up. Avoid redundant messages—they waste tokens and confuse the model. Efficiency is a feature."

---

## 📊 Metrics Dashboard

If this were production, I'd track:

| Metric | Result | Measurement |
|--------|--------|---|
| **Autonomy** | 20+ decisions without asking | # decisions made without human input |
| **Constraint adherence** | All 3 options within budget/distance/dates | % of options violating constraints |
| **Execution success** | Email sent + calendar updated | # deliveries / # events created |
| **User satisfaction** | User approved Option 1 | Approval rate on recommendations |
| **Efficiency** | One-message prompt | Tokens used per trip planned |
| **Safety** | Stopped for human approval | Prevented premature execution |

---

## 🔄 Version 2.0 Improvements

Current version (1.0):
- ✅ Autonomous search + planning
- ✅ Detailed itineraries
- ✅ Real email + calendar execution
- ❌ Can't handle feedback ("I don't like these options")
- ❌ Can't adjust budget mid-stream
- ❌ No preview/dry-run before booking

Version 2.0 would add:
1. **Feedback loop:** "Not happy? Tell me why (more hiking? lower budget? closer?) and I'll re-search"
2. **Dry-run mode:** Email + calendar appear as drafts for 24h review before confirmation
3. **Cost negotiation:** "Over budget? I'll swap the 3-star hotel for a budget option and re-show options"
4. **Proactive updates:** "Weather forecast shows rain Oct 5-6. Adjust the itinerary?"
5. **Multi-destination:** Plan multiple trips for different school holidays

---

## 🎤 My talking story

> "I built an autonomous trip recommender agent. What made it an agent: it didn't just recommend options—it autonomously executed on approval (sending emails and booking calendars). The hard part was distinguishing when to be autonomous (search, rank, evaluate) vs. when to ask humans (which destination?). This required clear constraints, intelligent approval gates, and measuring real outcomes like 'did the email actually deliver?' I learned that agent design is as much about safety and trust as it is about autonomy."

### "How I measured agent success?"

> "Not 'did it output text?' but 'did it complete the task?' In this case: did the email actually arrive? Did the calendar event actually appear? I also measure constraint adherence: stayed within budget? Respected school holidays? Drove less than 5 hours? That's how you prevent bad recommendations at scale."

### "Difference between an agent and a chatbot?"

> "A chatbot responds to queries. An agent pursues goals. My trip agent didn't just say 'here's a recommendation.' It autonomously searched, built options, ranked them, and executed on approval (email + calendar). The connectors matter—Gmail, Google Calendar—those are how it moves from language to action. Without execution, it's just a very sophisticated chatbot."

### "How did I handle failure or iterate?"

> "I noticed I initially wrote two chat messages thinking I needed both—system prompt plus user request. But Claude executed immediately after the first message. The second was redundant and wasted tokens. I learned to optimize based on observation. In production, I'd log every agent action (searches, emails, calendar updates) to see where it fails and iterate quickly."

### "How did I balance automation with human control?"

> "I built intentional approval gates. The agent autonomously plans and evaluates, but stops before committing money/calendar space to ask which option the user prefers. This is strategic autonomy—not 'no humans,' but 'humans at the right moments.' It prevents bad decisions while maintaining efficiency."

---

## 📁 GitHub Structure
