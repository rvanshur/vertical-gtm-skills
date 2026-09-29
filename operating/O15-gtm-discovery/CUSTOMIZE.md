# Customize: GTM Discovery

A paste-in prompt that adapts this skill to your market and stage.

Works in **Claude Code**, **Claude.ai Projects**, or **OpenAI Codex**, all three read the same `SKILL.md` format. Open the assistant, paste the block below, and answer its questions one at a time.

> This is a per-skill companion. For customizing the whole suite at once, see the README at `verticalgtmguild.com/skills`.

---

## The prompt

```
You are helping me adapt GTM Discovery to my specific market and stage.

Read the attached SKILL.md (gtm-discovery). It guides structured market discovery through eight independent modules: diagnostics, SWOT, problem mapping, beachhead segmentation, interview planning, competitive analysis, assumption mapping, and persona creation.

Your job is NOT to rewrite it. It is to make it fire on the customer and market I am actually selling into, and to help me identify which modules matter most for my stage.

Ask me these, ONE AT A TIME, and wait for each answer:

1. What are you building, and who do you think the customer is? (Product name, vertical, target customer role)

2. What stage are you at? (Idea, pre-launch, initial customers, growth mode, pivoting)

3. If you have already talked to customers, what is the one conversation that surprised you most? (What did you believe before, what did you learn?)

4. What do you believe about your customer that you have NOT yet tested? (List 3-5 assumptions that keep you up at night)

5. How much time do you have? (Can you run a full discovery engagement, or do you need the quick diagnostic?)

Then produce:

A. A prioritized module sequence, which discovery modules to run first, in order, with estimated time per module

B. A list of the three highest-risk assumptions (impact + lowest certainty) and the specific discovery method to test each one

C. A customer interview recruitment plan: where to find them, how many to talk to, and what the success metric is

D. THE HONEST PART: what you do not yet know about your market, and what would need to change for you to be confident in your beachhead

Start with question 1.
```

---

## What you should expect to happen

Most founders get through questions 1-3 smoothly. Question 4 stalls frequently.

That stall is the signal. The assumptions you cannot articulate are the ones that are wrong. They are also the ones that will cost you time and capital when the market finally teaches them to you.

Question 5 is the realism check. If you say "one week" but discovery is a two-month process, something has to give. Better to know that now than to run a shallow discovery and act on half-baked findings.

---

## Minimum profile fields this skill reads

Before running discovery, answer these once:

```markdown
## About Your Market

- **Vertical:** [Construction, property management, education, healthcare, etc.]
- **Target Customer Role:** [VP Sales, CFO, Operations Manager, etc.]
- **Estimated Market Size:** [Number of addressable companies]
- **Your Current Revenue:** [Zero, <$100K ARR, $100K-1M, etc.]
- **Urgency Level:** [How fast does the market move? Will customers still care in 6 months?]

## About Your Assumptions

- **Assumption 1 (Highest Risk):** [The belief that could kill your GTM if wrong]
- **How You'll Test It:** [Specific discovery method]
- **Success Metric:** [How you'll know if the assumption was right]

## Available Constraints

- **Time Budget:** [Hours per week you can spend on discovery]
- **Customer Access:** [Can you get warm introductions? Cold outreach? Do you have existing customers?]
```

---

## If you are stuck on any question

- **Question 1 stalls:** You do not yet have a clear product or customer. Start with `/gtm-discovery` module 3 (Problem Space). Let the customer's problems define who they are, rather than your guess about who they are.
- **Question 3 stalls:** You have not talked to customers yet. Stop here. Do not run the other modules. Go talk to 3-5 people in your target market. Come back when you have one surprising conversation.
- **Question 4 stalls:** You believe everything about your customer equally, or you do not know what you do not know. That is normal. Run module 7 (Assumption Mapping) first. It forces assumptions onto the table.
- **Question 5 stalls:** Be honest about time. A thorough discovery takes 2-4 weeks if you have customer access, 3-4 weeks if you do not. A quick diagnostic takes 4-6 hours. Underfunding discovery is how founders end up with the wrong customer hypothesis.

---

## Common patterns that indicate you are ready for the next skill

After running discovery, you should know:
- Who your specific customer is (role, company size, vertical, problem)
- What problem you are solving and how urgent it is
- What alternatives the customer is using now
- What segment you are entering first (narrow beachhead)
- Which of your assumptions are still untested

When you have that, you are ready for `/gtm-positioning`. It takes your discovery findings (customer, problem, competition) and builds a defensible market position from them.

If you skip to positioning without discovery, your position will be built on guesses instead of evidence. That always shows.
```
