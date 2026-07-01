# Introduction to System Design (தமிழில் விளக்கம்)

## System Design என்றால் என்ன?

System Design என்பது, ஒரு application-ஐ லட்சக்கணக்கான (millions) பயனர்கள் ஒரே நேரத்தில் பயன்படுத்தும்போது, அது எப்படி சரியாக, வேகமாக, நம்பகமாக (reliable) வேலை செய்யும் என்று திட்டமிடுவது.

ஒரு சாதாரண app, 10 பேருக்கு வேலை செய்யும். ஆனால் அதே app-ஐ 10 மில்லியன் பேர் பயன்படுத்தும்போது:

- ஒரே server crash ஆனா, முழு app-உம் நின்னுடும்
- Database-ல load அதிகமாகி, response slow ஆகும்
- New feature add பண்ண, existing system-ஐ உடைக்காம பண்றது கஷ்டமாகும்

இதை சமாளிக்கத்தான் System Design படிக்கிறோம்.

## இரண்டு வகைகள்

- **HLD (High-Level Design)** – Architecture level. Servers, database, load balancer, caching எப்படி ஒன்னோடு ஒன்னு connect ஆகுது.
- **LLD (Low-Level Design)** – Code level. Classes, design patterns.

Interview-ல "System Design Round" என்றா, பெரும்பாலும் HLD தான் கேட்பாங்க.

## மிக முக்கியமான Mindset - Trade-offs

System Design-ல "Perfect Solution" என்று ஒன்றும் கிடையாது. ஒவ்வொரு முடிவுக்கும் ஒரு trade-off இருக்கும்:

- Consistency வேணுமா, Availability வேணுமா?
- Cost குறைவா வேணுமா, Performance அதிகமா வேணுமா?

நீங்க ஒரு solution சொன்னா, ஏன் அதை தேர்ந்தெடுத்தீங்க, என்ன trade-off பண்ணீங்க என்று interviewer கேட்பாங்க. இதுக்கு பதில் தெரிஞ்சிருக்கணும்.

---

## Interview Preparation (English)

### Q1: How would you approach a system design interview question?

**A:** I'd follow a structured approach:

1. **Clarify requirements** – Ask about scale (number of users), read-heavy vs write-heavy traffic, latency expectations, and whether it's a functional or non-functional requirement discussion.
2. **Estimate scale** – Calculate approximate QPS (queries per second), storage needs, bandwidth.
3. **High-level architecture** – Draw the basic flow: Client → Load Balancer → Application Servers → Database/Cache.
4. **Deep dive** – Pick 1-2 critical components and discuss them in detail (e.g., database choice, caching strategy).
5. **Discuss trade-offs** – Explicitly call out what you're optimizing for and what you're sacrificing.

### Q2: What's the difference between HLD and LLD?

**A:** HLD focuses on system-level architecture — how major components interact, what technologies are used, and how the system scales. LLD focuses on the internal design of individual components — class structures, design patterns, and implementation details. In most system design interviews, the focus is on HLD.

### Q3: Why do we need system design at all — why not just use a bigger server?

**A:** Vertical scaling (bigger server) has physical and cost limits, and it creates a single point of failure. System design introduces horizontal scaling, redundancy, and distribution to handle failures gracefully and scale beyond what one machine can do.