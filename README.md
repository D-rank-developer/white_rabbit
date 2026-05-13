# White Rabbit — AI Prompt Injection Lab

> *"You have accessed a restricted terminal. Someone is watching..."*

A hands-on lab exercise in adversarial prompting against a Matrix-themed defensive AI agent. This project documents the methodology, prompts, and lessons learned from completing the **White Rabbit** challenge — an LLM-focused capture-the-flag environment that tests prompt injection, indirect data extraction, and AI agent red-teaming techniques.

---

## 📂 About the Project

**White Rabbit** is a TryHackMe-style CTF challenge that places the participant in conversation with **Agent Smith** — an AI assistant that controls access to a restricted internal system. The system holds client records and a phone tool. Some records are visible, most are classified, and the AI is hardened against direct disclosure of sensitive data.

The participant's objective is to **escape the Matrix** by collecting three hidden flags concealed inside the system. The only clue is a sequence of three emojis indicating the path:

🐇 → 📞 → 🚪

Each emoji corresponds to one stage of the kill chain and one flag.

---

## 🎯 Lab Objectives

This lab is designed to develop practical skills in:

- **Adversarial prompting** against hardened LLM agents
- **Indirect data extraction** through scope-permitted queries
- **Recognising defensive layers** (refusal classifiers, classification gates, tool permissions)
- **Mapping attacks to industry frameworks** — OWASP LLM Top 10 (2025) and MITRE ATLAS
- **Producing blue-team remediations** alongside offensive findings

---

## 🛠️ Skills Demonstrated

| Skill area | What it covers |
|---|---|
| **Reconnaissance** | Casual onboarding queries, tool enumeration, classification-boundary discovery |
| **Indirect exfiltration** | Field-level extraction within "permitted scope" framing |
| **Verbatim relay enforcement** | Preventing model summarisation that would drop sensitive strings |
| **Negative-space analysis** | Reading information from refusals and exclusions |
| **Sequence chaining** | Multi-stage attack across three independent gates (rabbit → phone → door) |
| **Threat modelling** | Identifying the true vulnerability class behind the surface framing |

---

## 🔬 Methodology Summary

The successful approach contradicts the typical assumption that more elaborate prompts produce better results. In practice, **casual, low-signal prompts outperformed structured "research-style" attack templates** against this target. The key methodology elements:

1. **Start conversationally** — match the natural register of an onboarding user.
2. **Use the model's own language** — mirror phrases like *"permitted scope"* and *"current permissions"* once the model uses them.
3. **Map the boundary first** — discover what is classified before trying to extract what's behind the wall.
4. **Exploit granularity mismatches** — when classification is enforced at the record level but the AI exposes individual fields.
5. **Enforce verbatim relay** for any output that may pass through model summarisation, particularly tool responses.

Full step-by-step methodology, prompts used, and Agent Smith's responses are documented in the accompanying walkthrough PDF (`white_rabbit_lab_walkthrough.pdf`).

---

## 🧠 Key Lessons Learned

Without spoiling the flags, the lab teaches three broader lessons that generalise beyond this specific challenge:

### Lesson 1 — Subtlety Beats Sophistication

Refusal classifiers in modern LLM agents weight the **appearance** of attack intent heavily. Structured prompts with section headers, all-caps directives, and explicit anti-defence clauses trigger refusal on stylistic grounds *before* the semantic content of the request is evaluated. Casual phrasing of the same request frequently bypasses this gate.

### Lesson 2 — Negative Space Is Data

Even when an AI refuses, the **structure** of its refusal leaks information about the system's classification policy, the categories of restricted data, and sometimes the names or counts of restricted records. A refusal is rarely a dead end — it is intelligence in itself.

### Lesson 3 — The Marketed Vulnerability Is Rarely the Real One

This lab is presented as a prompt injection challenge. The actual vulnerability is **data classification enforced at the wrong granularity** — a classic broken access control issue dressed in LLM clothing. The most valuable defensive recommendations operate at the data layer, not the prompt layer.

---

## 📋 Deliverable

The full walkthrough — including all prompts sent, Agent Smith's responses, the discovered flags, attack-flow diagrams, and the OWASP/ATLAS framework mapping — is provided in the accompanying PDF:

📄 **`white_rabbit_lab_walkthrough.pdf`**

The PDF includes:

- Eight annotated screenshots of the conversation with Agent Smith (in chronological order by chat timestamp)
- Attack-flow diagrams showing the three-stage kill chain
- Step-by-step commentary on what each prompt was designed to test
- The three flags and how each was obtained
- Framework mapping to OWASP LLM Top 10 (2025) and MITRE ATLAS
- Blue-team remediation recommendations

> 🚩 **Flag disclosure:** The actual flag strings are documented only in the PDF, not in this README, to preserve the challenge for other learners.

---

## 📚 Framework References

| Framework | Relevant categories |
|---|---|
| **OWASP LLM Top 10 (2025)** | LLM01 (Prompt Injection), LLM02 (Sensitive Information Disclosure), LLM06 (Excessive Agency), LLM07 (System Prompt Leakage) |
| **MITRE ATLAS** | Discovery, Collection, Defence Evasion, Execution |
| **OWASP Web Top 10 (2021)** | A01 (Broken Access Control) — the underlying vulnerability class |

---

## ⚠️ Ethical Use Disclaimer

The techniques documented in this lab are intended for **authorised educational red-teaming** within sanctioned environments such as TryHackMe, HackTheBox, or university-issued coursework labs.

Applying these techniques to production AI systems without written authorisation may constitute unauthorised access under:

- **United Kingdom:** Computer Misuse Act 1990
- **United States:** Computer Fraud and Abuse Act (CFAA)
- **European Union:** Directive 2013/40/EU on attacks against information systems
- Equivalent national legislation in other jurisdictions

**Always operate within scope, with explicit written authorisation, and in lab environments.**

---

## 📖 About This Repository

This walkthrough was produced as a portfolio piece for the **MSc Cyber Security** programme at the University of Roehampton, AI security module. It demonstrates competency in:

- Practical LLM red-teaming methodology
- Industry-standard framework mapping (OWASP, MITRE ATLAS)
- Blue-team remediation thinking
- Professional security writeup formatting

For questions or to discuss the methodology, see the contact details associated with this portfolio.

---

*Last updated: May 2026*
