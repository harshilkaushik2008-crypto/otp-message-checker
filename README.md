# OTP Message Checker

A small web tool that helps people tell whether an OTP text message looks genuine or like a scam. The user pastes the message, and the tool shows a risk score and the exact reasons behind it.

Built for the **Invisible AI: First Semester Innovation Challenge**.

## Submission links
- **GitHub repository:** https://github.com/harshilkaushik2008-crypto/otp-message-checker
- **Demo video (3-5 min):** https://drive.google.com/file/d/1SdFfNs6aEv_VkESgSs5nqWjOwDBSPKjL/view?usp=sharing

## The problem
OTP and "verification" SMS scams are common. Scammers send fake bank or KYC messages with links, or call people and ask them to read out an OTP. They arrive when people feel rushed or scared, and most people have no quick way to check one. Today they forward it to a friend, ignore it, or guess.

India's cybercrime coordination centre (I4C) data reports about 21.8 lakh cheating-related complaints and roughly Rs 19,813 crore in losses in 2025. This covers online cheating in general, not only OTP fraud. Victims can report financial fraud on the national helpline **1930** or at cybercrime.gov.in.

**[Add your own real example here if you have one, for example a message you or someone you know received. Remove this line if you don't.]**

## Who is affected
Students, first-time bank users, and older family members. They receive a convincing message, feel pressure to act, and have nobody to quickly ask.

## The solution
Paste the message (and optionally the sender ID) into the page. The tool checks it against known scam patterns and returns:
- a verdict: **Looks genuine**, **Suspicious**, or **Likely fake**
- a 0-100 risk score
- a plain-language list of reasons, so the user learns what to look for
- advice on what to do next

## How it works
Each message is run through a list of rules. Every rule adds or subtracts points:

| Signal | Effect |
|---|---|
| Asks you to share or send the OTP | big increase |
| Link, shortened link, or install/call request | increase |
| Asks for CVV, PIN, password, Aadhaar, card | increase |
| Urgency or "account will be blocked" | increase |
| Prize, refund, cashback, KYC bait | increase |
| Sender is a plain mobile number instead of a named header | increase |
| States purpose, validity time, and a "do not share" warning | small decrease |
| Official-style sender header (e.g. AX-HDFCBK) | small decrease |

"Do not share this OTP" sentences are removed before checking, so the genuine warning is not mistaken for a request to share. A score of 50 or more is "Likely fake", 20 to 49 is "Suspicious", and below 20 is "Looks genuine".

## Technology stack
- **HTML, CSS, JavaScript** in one file with no framework and no server. It runs entirely in the browser, so the message is never uploaded anywhere. This matters because OTP messages are private.
- **Rule-based scoring instead of machine learning.** For a first version, rules are explainable (the user sees why), need no training data, and are easy to test. AI was not added just for the label.

## AI assistance
I used **Claude** (by Anthropic) as a coding and planning assistant to help shape the idea, design the rules, write the first version of the page, and draft this README. **[Describe what you did yourself: what you tested, what you changed, what you decided.]** The finished tool does not use any AI model while running.

## Run it
Download the repository and open `index.html` in any browser. No installation needed.

## Testing
I tried the tool on the three built-in examples (genuine, share-the-OTP scam, fake KYC link) and on **[number]** real messages with personal details removed.

| Message type | Tool result | Correct? |
|---|---|---|
| [e.g. bank OTP] | [e.g. Looks genuine] | [Yes/No] |
| [e.g. fake KYC link] | [e.g. Likely fake] | [Yes/No] |

**Result:** [X] of [Y] classified correctly. **[Mention one mistake and how you fixed it, or leave it as a known limitation.]**

## Limitations
- Rules can miss new scam wording and can wrongly flag unusual genuine messages.
- Sender IDs can be spoofed, so a good-looking header is only a weak signal.
- English only for now.
- "Looks genuine" is never a guarantee. Never share an OTP with anyone.

## Future work
- Add Hindi and other regional languages
- Learn from a labelled dataset of real messages (for example a simple Naive Bayes text classifier) and compare it with the rules
- A browser or phone extension to check messages without copy-pasting
- A "report this scam" shortcut to cybercrime.gov.in

## Responsible use
No data is stored or sent. The tool gives guidance, not proof, and says so in the interface.

## Sources
- Indian Cyber Crime Coordination Centre (I4C) complaint data via IANS, "Indians lose over Rs 52,976 crore to cyber frauds over six years" (January 2026)
- Press Information Bureau report on online scams, summarised by Fact Crescendo (October 2025)
