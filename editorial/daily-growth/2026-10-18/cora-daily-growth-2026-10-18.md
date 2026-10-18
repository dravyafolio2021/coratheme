# Cora Daily Growth Handoff — 18 October 2026

Status: Editorial handoff; nothing in this package is published. Coding work is specified, not implemented.

## Executive brief

Today’s organic cluster is **agency cash collection**: payment terms, deposits, milestone billing, days sales outstanding (DSO), invoice approval and overdue-work policies. It is distinct from the recent Cora clusters on revenue forecasting, client profitability, retainer health, scope creep and renewals. The opportunity is commercially close to Cora’s invoicing, CRM, contracts and workflow capabilities without pretending Cora is an accounting, legal or debt-collection service.

The first-party case is a gap rather than an existing winner. Search Console for 18 September–17 October returned 112 query/page rows but none for agency payment terms, DSO, milestone billing or late-payment collection. GA4 recorded 226 sessions across 17 landing pages, with zero key events; `/partners/agencies` drew 19 sessions and 94.74% engagement, while the two existing agency articles drew only three sessions combined. This cluster should therefore create focused discovery entry points and route them to an instrumented tool, not merely add generic blog volume.

Evidence guardrails: MSME Samadhaan states a buyer’s delayed-payment liability can arise beyond the applicable acceptance/payment period and references 45 days; legal eligibility depends on facts and current law. Cora content must say “check your registration, contract and adviser” and must not turn the calculator into legal advice. The official Cora pricing page showed Professional at ₹24,990/year on 18 October 2026; the plan card and footer conflict on tax treatment, so copy should use the annual value only and make no GST-inclusive/exclusive claim.

## 1. Free tool requirements document

### Product name

**Agency Invoice Cash-Flow Gap Calculator**

Proposed route: `/tools/agency-invoice-cash-flow-calculator`

### User problem and job to be done

An agency can be profitable on paper and still run short of cash because payroll and contractor costs occur before deposits, milestones or retainers arrive. Standard invoice generators answer “what is owed?” They do not answer the operating question: **Will this engagement create a cash gap, when will it peak, and which billing schedule reduces exposure without inventing revenue?**

The tool lets an owner compare realistic payment schedules before signing a statement of work or changing terms. It does not forecast sales, score a client’s creditworthiness, calculate taxes, or promise collection.

Primary ICP:

- Indian creative, marketing, web, software and consulting agencies with 2–50 people.
- Founder-led studios using fixed-fee projects, retainers or milestone engagements.
- Operations and finance leads who need a defensible schedule for proposals and client conversations.

Secondary ICP: freelancers moving into multi-person delivery.

### Core workflow

1. Choose engagement type: fixed-fee project, monthly retainer or mixed.
2. Enter currency, contract value and project start/end dates.
3. Enter expected cash outflows by month: payroll allocation, contractors, software, media/pass-through costs and other direct costs. Taxes are explicitly excluded from spendable cash by default.
4. Build the current billing schedule. Each receipt has a trigger (signature, date, delivery milestone or recurring cycle), invoice date, amount/percentage, contractual terms and expected extra delay based on experience.
5. Select comparison presets: 0/50/50, 30/40/30, 50/25/25, 100% upfront, monthly prepaid retainer, monthly arrears, or custom.
6. View the cash curve, maximum cumulative funding gap, days exposed, receivables at completion and schedule comparison.
7. Export a one-page planning summary or copy a client-safe payment schedule. Email is optional and appears only after useful results exist.

### Inputs

Required:

- Engagement type.
- Currency (default INR; no FX conversion).
- Contract value excluding tax.
- Start and planned completion dates.
- At least one cost item or monthly cost total.
- At least one payment event whose percentages total 100%.
- Contractual payment term in days.

Optional:

- Deposit already received.
- Expected invoice issue delay.
- Historical client delay beyond terms.
- Holdback/retention percentage.
- Pass-through spend and whether client prepays it.
- Contingency buffer.
- India MSME information toggle, with non-advisory explanation and official link.
- Scenario label and client/project nickname; warn users not to enter confidential personal data.

### Calculations and outputs

Use daily dates internally and monthly buckets for the default chart.

- Expected receipt date = invoice date + contractual term + expected extra delay.
- Net cash per period = expected receipts − cash outflows.
- Cumulative cash position starts at zero unless an opening project reserve is entered.
- Maximum funding gap = absolute value of the most negative cumulative position; zero if never negative.
- Exposure days = number of days cumulative position is below zero.
- Receivables at project completion = invoiced but not expected received by completion.
- Cash-conversion lag = weighted average days from delivery trigger to expected receipt, labelled as a planning measure rather than accounting DSO.
- Break-even receipt date = first date cumulative project cash becomes non-negative and remains so.
- Comparison ranks schedules by smallest maximum gap, then shortest exposure, without calling one “best.”

Result cards:

1. Peak cash gap and date.
2. Days the project is self-funded.
3. Cash collected before work begins.
4. Receivables outstanding at planned completion.
5. Suggested discussion points: deposit, pass-through prepayment, smaller milestones, invoice prerequisites and pause-work clause.

### Edge cases

- Percentages do not total 100: disable calculation and identify the variance.
- Negative or zero values: reject except opening reserve may be zero.
- Receipt before invoice or milestone before project start: inline validation.
- Same-day events: aggregate for chart but preserve line items.
- End date before start date, leap day and timezone boundaries: date-only arithmetic in the selected locale.
- Contract value and payment amounts differ by rounding: allocate residual to final payment and disclose it.
- Retainer with no end date: require a planning horizon of 3, 6 or 12 months.
- Very long terms or delay: support up to 365 days, show a high-exposure warning, do not provide a legal conclusion.
- Holdback beyond horizon: show as outstanding, never as collected.
- Refunds, credit notes, bad debt, financing and foreign exchange: out of scope for v1; explain rather than silently miscalculate.
- Tax: values are excluding tax and collected tax is not available operating cash. Do not provide GST advice.
- MSME toggle: show informational text only. Never assert eligibility, calculate statutory interest or recommend litigation.

### UX requirements

- Desktop: two-column builder/result view; mobile: a four-step wizard with a sticky “Calculate” action.
- Start with a worked example rather than an empty spreadsheet.
- Make presets editable and show the cash curve updating immediately.
- Chart: time on x-axis, cumulative project cash on y-axis, zero line, receipt markers and cost bands. Also provide an accessible table and written summary.
- Use plain labels: “Expected extra delay” instead of “delinquency,” “Peak cash gap” instead of “working-capital deficit.”
- Provide “Reset,” “Duplicate scenario,” “Compare,” “Download PDF,” and “Copy schedule.”
- Persist locally in the browser by default; offer deletion. Server storage requires explicit sign-in.
- Meet WCAG 2.2 AA: keyboard operation, visible focus, text alternatives, error summary, non-colour risk indicators and reduced-motion support.
- Never gate the calculation. Lead capture may gate only the enhanced PDF/template bundle.

### SEO landing page

- Title: `Free Agency Cash Flow Gap Calculator | Cora`
- Meta description: `Compare deposits, milestones and payment terms. See an agency project’s peak cash gap, exposure days and expected receipt timeline—free.`
- H1: `See the cash gap before you sign the project`
- Intro must answer what the calculator does in 45–65 words, then place the interactive tool above the fold.
- Supporting sections: how it works; formulas; deposit vs milestone examples; prepaid vs arrears retainers; invoice prerequisites; India MSME information; FAQ; limitations; related Cora workflows.
- Schema: `SoftwareApplication`, `FAQPage` only for visible FAQs, and `BreadcrumbList`. Do not add fabricated reviews or ratings.
- Canonical must be self-referencing; indexable result shell but no query-string scenario pages in the index.
- Internal links: invoicing feature/docs, contracts, CRM, `/partners/agencies`, the ten articles below and all three guides.
- AI discovery: include concise definitions for peak cash gap, payment terms and planning DSO; use an example with explicit assumptions; publish formula text in HTML, not only canvas/SVG.

### Beehiiv and lead capture

Keep the core calculator anonymous. After results, offer **“Email me the editable Payment Schedule + Collection Checklist.”** Capture work email and optional agency size with explicit newsletter consent separate from asset delivery. Deliver a Beehiiv-hosted or transactional link; do not subscribe users unless the checkbox is selected.

Beehiiv tags/custom fields: `source=agency-cash-gap-tool`, `asset=payment-schedule-kit`, `engagement_type`, `cash_gap_band` (bucketed, never exact sensitive value), `consent_timestamp`, and UTM fields. Suggested five-email sequence: results interpretation; invoice prerequisite checklist; deposit/milestone guide; overdue ladder; Cora workflow demonstration. Every marketing email needs unsubscribe controls.

### Analytics events

| Event | Trigger | Safe parameters |
|---|---|---|
| `cash_gap_tool_view` | Tool becomes visible | referrer_group, device |
| `cash_gap_example_load` | Example selected | example_type |
| `cash_gap_calculate` | Valid calculation | engagement_type, currency, term_band, gap_band |
| `cash_gap_validation_error` | Submission blocked | error_code, step |
| `cash_gap_scenario_compare` | Comparison displayed | scenario_count, winning_gap_band |
| `cash_gap_result_expand` | Explanation opened | card_name |
| `cash_gap_export_pdf` | Export succeeds | engagement_type |
| `cash_gap_copy_schedule` | Copy succeeds | schedule_type |
| `cash_gap_lead_open` | Asset form opened | placement |
| `cash_gap_lead_submit` | Asset delivery succeeds | consent_boolean, agency_size_band |
| `cash_gap_cora_cta` | Product CTA clicked | placement, result_state |

Never send client names, exact contract values, emails or free text to analytics.

### Acceptance criteria

- All supported schedules total 100% and produce deterministic daily and monthly results.
- Automated tests cover every formula, rounding, dates, retainers, holdbacks and invalid inputs.
- Three reference scenarios are hand-checked against a spreadsheet; all results match to the smallest displayed currency unit.
- Changing expected delay changes receipt dates and exposure, not contract value.
- The tool works without login, email or network after initial load.
- PDF and copied schedule repeat assumptions and the non-advisory disclaimer.
- No user-entered project data enters analytics.
- Lighthouse targets on a mid-tier mobile profile: performance ≥90, accessibility ≥95, SEO ≥95.
- Keyboard-only and screen-reader test passes all steps, chart alternative and errors.
- Lead submission records consent independently and does not subscribe an unchecked user.
- SEO copy, schema, canonical, sitemap and internal links ship with the tool.
- Legal review approves MSME informational copy before launch; if not approved, hide the India toggle without blocking the calculator.

## 2. Ten publish-ready articles

### Article 1 — Agency Payment Terms: How to Get Paid Without Making Good Clients Defensive

**Primary keyword / intent:** agency payment terms / commercial investigation.  
**Slug:** `/articles/agency-operations/agency-payment-terms`  
**Meta title:** `Agency Payment Terms: A Practical Guide`  
**Meta description:** `Choose deposits, due dates, milestones and pause-work rules that protect agency cash flow while staying clear and fair to clients.`  
**Status:** Ready for editorial/legal review.

Revenue is not cash. An accepted proposal can look excellent while the agency funds four weeks of payroll before the first receipt. Payment terms are the operating design that closes that gap.

Start with four dates: when work begins, when the invoice may be issued, when it is contractually due, and when clients actually pay. “Net 30” only describes one interval. If procurement takes ten days to create a vendor record and the agency waits five days after a milestone to invoice, a 30-day term can become a 45-day cash wait.

For projects, collect a deposit before reserving capacity. Tie later invoices to objective events the client can verify: kickoff, approved direction, staging delivery or handover. Avoid vague triggers such as “near completion.” For retainers, invoice before the service month when capacity is reserved in advance. Arrears can suit usage-based work, but it transfers more funding risk to the agency.

Write each term in operational language: amount, trigger, invoice recipient, required purchase-order number, due date, accepted payment methods, approver, dispute window, late-payment consequence and when work may pause. Put the same essentials in the proposal, contract and invoice so the client does not discover a rule after work starts.

Do not choose the shortest term merely because it is protective. A large client may genuinely need procurement time. The better negotiation is to change the schedule: a larger deposit, prepaid third-party costs, smaller milestones, or an approval deadline. The aim is a fundable engagement, not an adversarial contract.

Before signing, model the expected receipt dates against delivery costs. If the cumulative project balance goes negative, the agency is lending to the project. Change the structure while goodwill is high.

**Internal links:** cash-gap calculator; contracts; invoicing; Article 2; Guide 1.  
**CTA:** `Compare your current terms with two alternatives in the free Agency Invoice Cash-Flow Gap Calculator.`  
**Sources:** Australian Government payment-terms guidance; MSME Samadhaan; Cora calculator methodology.  
**Cover/OG brief:** Clean timeline from signature to cash receipt, with invoice and payroll markers; Cora sky-blue field, navy type, no currency pile imagery.

### Article 2 — Deposit vs Milestone Billing for Agencies

**Primary keyword / intent:** deposit vs milestone payment / solution comparison.  
**Slug:** `/articles/agency-operations/deposit-vs-milestone-billing`  
**Meta title:** `Deposit vs Milestone Billing for Agency Projects`  
**Meta description:** `Learn when deposits, milestones or upfront billing fit an agency project—and how to compare their cash-flow exposure.`  
**Status:** Publish-ready after legal review.

A deposit answers one question: how much commitment should exist before the agency reserves capacity? Milestone billing answers another: how should the remaining value be collected as risk changes?

Use a meaningful deposit when the agency must decline other work, hire contractors, buy media or begin discovery immediately. A token amount may confirm intent without funding delivery. A very large upfront request may be hard for a new client to approve. The right level depends on costs and bargaining position, not an internet rule.

Milestones work when they are observable and reasonably spaced. A 30/40/30 schedule could mean 30% at signature, 40% when the agreed direction is approved and 30% before final handover. It becomes dangerous when the middle trigger depends on subjective approval that can drift indefinitely. Add an approval window and a rule for consolidated feedback.

Time-based billing can be safer than deliverable-based billing when delays are mostly client-controlled. For example, invoice every two weeks against completed work, with a not-to-exceed cap. For retainers that reserve a team, prepaid monthly billing usually matches the economic reality better than waiting until month-end.

Compare schedules using three measures: cash collected before the largest cost period, the maximum cumulative cash gap and receivables still open at completion. A schedule that looks balanced as percentages may still be poorly timed.

Keep pass-through costs separate. Media, printing, licences and specialist expenses should usually be prepaid or directly purchased by the client. Otherwise the agency earns no return for financing somebody else’s spend.

**Internal links:** calculator; Article 1; Article 6; Guide 2.  
**CTA:** `Load the 30/40/30 and 50/25/25 presets and compare the cash curve.`  
**Sources:** Australian Government payment-terms guide; general invoicing anatomy from Invoice Generator; Cora methodology.  
**Cover/OG brief:** Three stacked milestone blocks crossing a zero-cash line; use percentages, not specific revenue claims.

### Article 3 — DSO for Agencies: The Metric Behind “Busy but Cash-Poor”

**Primary keyword / intent:** agency DSO / informational-commercial.  
**Slug:** `/articles/agency-finance/dso-for-agencies`  
**Meta title:** `DSO for Agencies: Formula, Limits and Actions`  
**Meta description:** `Calculate days sales outstanding, understand why agency DSO rises, and build an operational plan to collect faster.`  
**Status:** Publish-ready.

Days sales outstanding estimates how long credit sales remain uncollected. A common formula is:

`DSO = average accounts receivable ÷ credit revenue × days in period`

If average receivables are ₹12 lakh, credit revenue is ₹60 lakh and the period has 90 days, DSO is 18 days. That is a portfolio measure, not a promise about any invoice.

Agencies should pair DSO with the invoice-level picture. A low portfolio DSO can hide one large overdue account; a high DSO can reflect intentionally long enterprise terms. Track median days-to-pay, percentage overdue, receivables concentrated in the top client and the difference between contractual terms and actual payment.

When DSO rises, inspect the process before blaming clients. Was the invoice issued immediately? Did it contain the PO, tax details and legal entity the buyer requires? Did it reach the approver? Was the milestone accepted? Is the client disputing scope? Is the team continuing work while an invoice remains unresolved?

Improvements usually come from removing delay at several points: confirm billing data during onboarding, invoice on the trigger date, provide a payment link or bank details, send a reminder before due date, assign an owner, escalate predictably and review chronic exceptions before renewal.

Do not optimize DSO in isolation. Forcing every trusted client into an impractical term can damage good relationships. The useful target is consistency between the terms priced into the engagement and the cash behavior the agency can fund.

**Internal links:** calculator; invoice approval article; collections guide; client profitability content.  
**CTA:** `Calculate project-level cash exposure, then add DSO to your monthly agency scorecard.`  
**Sources:** Association for Financial Professionals DSO definition; Intrum 2026 DSO guide; Atradius on invoice accuracy and credit policy.  
**Cover/OG brief:** Receivables clock with a portfolio bar and one highlighted overdue account; analytical, not alarmist.

### Article 4 — A Late-Invoice Follow-Up Sequence That Protects the Relationship

**Primary keyword / intent:** late invoice follow up agency / template-seeking.  
**Slug:** `/articles/agency-operations/late-invoice-follow-up-sequence`  
**Meta title:** `Late Invoice Follow-Up Sequence for Agencies`  
**Meta description:** `Use a calm, documented overdue-invoice sequence with clear owners, escalation points and stop-work decisions.`  
**Status:** Publish-ready after legal review.

Collections become emotional when the agency improvises. A written sequence makes the process calmer for both sides.

Three business days before due: confirm the invoice is in the right system and ask whether anything blocks approval. On the due date: send a short reminder with invoice number, amount, due date and payment route. Three to five days late: ask for a specific payment date and copy the operational sponsor if accounts payable is silent. Seven to ten days late: summarise the history, identify the contract clause and schedule a decision with the agency owner. At the pre-agreed threshold: pause new work or handover only if the contract and local advice support it.

Every message should separate facts from frustration. “Invoice 104 was due on 12 October and remains open” is useful. “You always ignore us” is not. Ask one clear question: “Can you confirm the payment date today?”

Maintain a collection record: invoice, delivery evidence, approvals, reminders, client responses and promised dates. If the client disputes quality or scope, move the issue into a named resolution workflow rather than repeating payment reminders.

Never threaten statutory interest or legal action casually. Rights vary by jurisdiction, registration and contract. Indian micro and small enterprises may have remedies for delayed payments, but eligibility and procedure require current professional guidance.

The strongest collection system begins before the invoice: correct legal entity, procurement contact, PO requirement, approver, dispute window and pause-work rule. Recovery is a backstop, not a billing strategy.

**Internal links:** Article 8; Article 9; Guide 3; contracts.  
**CTA:** `Download the editable reminder ladder and decision log through the Cash Collection Playbook.`  
**Sources:** MSME Samadhaan; Australian Government payment-terms guide.  
**Cover/OG brief:** Five-step escalation ladder from confirmation to decision, with neutral envelopes and check marks.

### Article 5 — Prepaid vs Arrears Retainers: A Cash-Flow Decision

**Primary keyword / intent:** prepaid vs arrears retainer / comparison.  
**Slug:** `/articles/agency-finance/prepaid-vs-arrears-retainer`  
**Meta title:** `Prepaid vs Arrears Agency Retainers`  
**Meta description:** `Compare prepaid and arrears retainers by capacity, usage, cash exposure and client procurement constraints.`  
**Status:** Publish-ready.

Prepaid and arrears billing describe when cash moves, not whether a retainer is fair.

Prepaid billing fits capacity retainers. The agency reserves a defined team, response time or monthly output whether or not every hour is used. The client pays before the service period because capacity cannot be resold after the month passes.

Arrears fit variable usage that cannot be known in advance. It can also satisfy enterprise procurement, but the agency funds delivery until the invoice clears. If actual payment arrives 45 days after month-end, January work may become March cash.

A hybrid reduces uncertainty: a prepaid base covers committed capacity, while approved overages are billed in arrears. Another option is a replenishing credit balance. Whatever the structure, define rollover, overage approval, paused work, unused capacity and cancellation.

Compare the models over six months. Plot payroll and contractor costs against expected receipt dates, including historical client delay. The difference is the working capital the agency provides. If the client needs arrears, price and risk approval should reflect the exposure rather than hiding it.

Do not call every recurring invoice a retainer. A prepaid package with unlimited obligations creates delivery risk; an arrears time-and-materials arrangement creates collection risk. The contract needs a measurable service boundary.

**Internal links:** calculator; Article 1; retainer-health content; Guide 1.  
**CTA:** `Model a prepaid, arrears and hybrid scenario before your next renewal.`  
**Sources:** Cora scenario methodology; Australian Government contract/payment-term guidance.  
**Cover/OG brief:** Split calendar showing cash before service vs after service, with a hybrid band in the middle.

### Article 6 — Cash-Flow Forecasting for Fixed-Fee Agency Projects

**Primary keyword / intent:** agency project cash flow forecast / how-to.  
**Slug:** `/articles/agency-finance/project-cash-flow-forecast`  
**Meta title:** `Cash-Flow Forecasting for Agency Projects`  
**Meta description:** `Build a simple project cash forecast using delivery costs, invoice triggers, payment terms and realistic client delay.`  
**Status:** Publish-ready.

A project budget tells you whether the work may be profitable. A project cash forecast tells you whether the agency can fund it.

Create a dated list of costs: internal payroll allocation, contractors, software, production and pass-through spend. Then create a dated list of receipts. Use expected bank dates, not invoice dates. Add procurement lead time and the client’s observed delay beyond terms.

Calculate the cumulative balance after each event. The lowest point is the peak project cash gap. Count how many days the balance remains negative and how much is still receivable at planned completion. Run a delayed scenario—perhaps 14 days beyond terms—not because it will happen, but because the agency needs to know whether it can absorb it.

Use the result to redesign the schedule. Move a deposit to signature, prepay third-party costs, create a milestone before the largest delivery month or split one large completion invoice into smaller objective stages. Do not solve the gap by assuming an uncontracted upsell.

Review the forecast at kickoff and whenever timing changes. If a milestone slips, update both costs and receipts. A living forecast can trigger a commercial conversation before the bank balance becomes the messenger.

Keep tax and pass-through money separate from operating cash. The model is a planning view, not a substitute for accounting records or professional advice.

**Internal links:** calculator; Article 2; revenue forecasting guide; Guide 2.  
**CTA:** `Build the cash curve with your real milestone dates in under five minutes.`  
**Sources:** AFP DSO definition; Cora calculator methodology.  
**Cover/OG brief:** Two lines—costs and receipts—forming a highlighted negative gap; restrained finance graphic.

### Article 7 — Change Orders That Get Scope and Billing Back in Sync

**Primary keyword / intent:** agency change order process / operational template.  
**Slug:** `/articles/agency-operations/change-order-billing-process`  
**Meta title:** `Agency Change Orders: Scope, Price and Billing`  
**Meta description:** `Turn out-of-scope requests into clear change orders with delivery impact, approval and payment triggers.`  
**Status:** Publish-ready.

A change order is not merely a price quote. It reconnects scope, schedule, capacity and cash.

When a request changes the agreement, record the requested outcome, what is added or removed, assumptions, delivery impact, fee, payment timing and the person authorised to approve it. Mark affected work as pending until approval. This prevents the team from treating a friendly chat message as funded scope.

Small changes can use a lightweight form. Larger changes need a revised milestone plan. If the added work requires a contractor or extends the project, collect the corresponding amount before committing the cost. If it shifts the final invoice later, consider an interim milestone.

Avoid punitive language. Explain the consequence: “This adds two design rounds and moves launch by one week. The change fee is ₹X, invoiced on approval.” Give the client a choice—approve, swap an existing item or defer it.

Link the approved change to the project record and invoice. The delivery team should see one source of truth; finance should not reconstruct scope from chat threads. Review cumulative change value, approval time and unpaid change work each month.

**Internal links:** scope-creep article; calculator; contracts; Guide 2.  
**CTA:** `Add the revised invoice event to the calculator before approving the change.`  
**Sources:** Existing Cora scope-creep content; general contract/payment-term guidance.  
**Cover/OG brief:** Change request card flowing into scope, timeline and invoice—three connected panels.

### Article 8 — The Client Invoice Approval Checklist Agencies Forget

**Primary keyword / intent:** client invoice approval process / troubleshooting.  
**Slug:** `/articles/agency-operations/client-invoice-approval-checklist`  
**Meta title:** `Client Invoice Approval Checklist for Agencies`  
**Meta description:** `Prevent avoidable invoice delays by confirming entity, PO, approver, milestone evidence and payment route before kickoff.`  
**Status:** Publish-ready.

Many late invoices were delayed before they were issued. The agency lacked a vendor record, used the wrong legal entity, omitted a PO or sent the invoice to the project sponsor instead of accounts payable.

During onboarding, confirm: billing entity and address; tax identifiers; PO or vendor-registration requirement; invoice portal; accounts-payable email; commercial approver; milestone evidence; accepted currency and payment method; dispute window; expected payment run; and who can unblock an exception.

Before each invoice, check the contract trigger, approval evidence, line-item description, tax treatment, PO balance, client reference, bank details and due date. Submit through the required route and retain confirmation. Then tell the sponsor it has been submitted.

Create one owner for the receivable. A shared inbox without ownership is not a system. The owner tracks acceptance, due date, promised date and dispute reason. If the client changes entity or procurement system, update the master record before the next cycle.

This checklist is deliberately boring. That is why it works: it removes preventable uncertainty so the relationship is reserved for real commercial decisions.

**Internal links:** onboarding article; invoicing; Article 4; Guide 1.  
**CTA:** `Get the client-ready invoice prerequisite sheet in the Cash Collection Playbook.`  
**Sources:** Atradius on invoice accuracy and DSO; Australian Government payment-terms guidance.  
**Cover/OG brief:** Minimal checklist beside an invoice route: project sponsor → AP → approver → payment.

### Article 9 — When Should an Agency Pause Work for Non-Payment?

**Primary keyword / intent:** pause work for nonpayment agency / decision support.  
**Slug:** `/articles/agency-operations/pause-work-for-nonpayment`  
**Meta title:** `When to Pause Agency Work for Non-Payment`  
**Meta description:** `Use a contract-backed decision framework for overdue invoices without making impulsive threats or abandoning client context.`  
**Status:** Requires legal review before publication.

Pausing work is a risk decision, not an automated punishment. The agency must consider the contract, local law, disputed work, client communication, dependency risk and the cost of continuing.

Create thresholds before an invoice is late. For example: friendly confirmation before due date; owner review at five days late; executive escalation at ten; pause decision at a stated threshold. The exact numbers belong in the contract and should reflect project size and client type.

Before pausing, verify the invoice is correct, the trigger occurred, the client received it, procurement requirements were met and no genuine dispute is open. Ask for a documented payment date. Assess what a pause affects: live campaigns, security, data, statutory duties and third parties may need a controlled transition rather than an abrupt stop.

If the decision is to pause, communicate the facts, contractual basis, affected activities, safe state and restart condition. Preserve work and access appropriately. Do not hold client data hostage or make legal threats without advice.

The commercial lesson should feed forward. Chronic exceptions may require a larger deposit, prepaid retainer, shorter milestone interval, credit limit or a decision not to renew.

**Internal links:** Article 4; contracts; offboarding guide; Guide 3.  
**CTA:** `Use the overdue decision tree in the Late Payment Prevention & Recovery Playbook.`  
**Sources:** MSME Samadhaan; Australian Government contract guidance.  
**Cover/OG brief:** Decision tree with verify, escalate, pause and resume nodes; no gavel or threatening imagery.

### Article 10 — Agency Billing Cadence: Weekly, Milestone or Monthly?

**Primary keyword / intent:** agency billing cadence / comparison.  
**Slug:** `/articles/agency-finance/agency-billing-cadence`  
**Meta title:** `Agency Billing Cadence: Weekly, Milestone or Monthly?`  
**Meta description:** `Choose a billing cadence based on delivery certainty, client approvals, cash exposure and administrative load.`  
**Status:** Publish-ready.

Billing cadence determines how often delivery becomes a receivable. The right cadence matches how value and risk accumulate.

Weekly or fortnightly billing fits rapid, variable work and limits exposure, but increases administration. Milestone billing fits projects with observable stages, provided approvals cannot drift. Monthly prepaid billing fits reserved capacity. Monthly arrears fits measurable usage but asks the agency to finance the month plus the payment term.

Evaluate four dimensions: how predictable the scope is, how often the client can approve, when costs occur and how much unbilled work the agency can tolerate. Then count the operational burden. An elaborate schedule that finance cannot administer will fail.

Set a minimum billable event, a fixed invoice day and a cut-off for approved changes. Automate reminders, not judgment. A client dispute or changed milestone needs a human owner.

Run the proposed cadence through a delayed-payment scenario. If one missed approval creates an unacceptable gap, shorten the interval or increase the upfront amount. Billing architecture is part of delivery design.

**Internal links:** calculator; Article 2; Article 5; Guide 2.  
**CTA:** `Compare weekly, milestone and monthly scenarios with the free calculator.`  
**Sources:** Australian Government payment-terms guide; Cora methodology.  
**Cover/OG brief:** Three calendar lanes with equal project value but different receipt timing.

## 3. Three publish-ready guides and lead magnets

### Guide 1 — The Agency Cash Collection Playbook

**Keyword / intent:** agency cash collection process / high-intent operational.  
**Slug:** `/guides/agency-cash-collection-playbook`  
**Meta title:** `Agency Cash Collection Playbook + Templates`  
**Meta description:** `Build a clear agency collection system from onboarding and invoicing through reminders, disputes and monthly review.`  
**Editorial status:** Ready after legal review.

**Chapter structure:** 1) Design the terms; 2) Capture billing prerequisites; 3) Issue correctly; 4) Follow up before and after due; 5) Resolve disputes; 6) Escalate and pause; 7) Review metrics.

#### Full guide copy

Cash collection should feel like an operating process, not a monthly emergency. The strongest system begins at sale. Decide whether the engagement reserves capacity, reimburses usage or delivers defined milestones. Match the payment model to that reality and test it against costs.

At contracting, record the deposit, each trigger, terms, accepted methods, dispute window, late-payment language and pause-work rule. For Indian micro and small enterprises, delayed-payment provisions may be relevant, but registration, acceptance dates, agreements and remedies require current professional advice. Link to official MSME Samadhaan rather than summarising a legal outcome as guaranteed.

At onboarding, complete the billing passport: client legal entity, tax identifiers, AP contact, sponsor, approver, PO, portal, payment run, evidence requirements and escalation owner. No project enters delivery with an incomplete passport unless an owner accepts the risk.

At the billing trigger, issue on the same business day. Attach the evidence the client agreed to receive. Confirm portal acceptance and notify the sponsor. Record invoice date, contractual due date, expected date, balance and owner in one system.

Run a humane reminder ladder. Before due, ask whether anything blocks approval. On due date, provide the invoice facts and payment route. After due, ask for a specific date. Escalate to the commercial sponsor only after the normal AP route has had a fair chance. A dispute leaves the generic reminder lane and gains a named resolution owner, issue, evidence, next action and deadline.

Use a pause decision tree. Verify the invoice and delivery trigger. Check contract and local advice. Assess operational safety and third-party impact. Decide whether to continue, narrow or pause. Communicate the safe state and restart condition. Preserve the client’s data and rights.

Review monthly: portfolio DSO, median days-to-pay, percentage overdue, concentration, disputed value, invoices issued late and promises missed. Segment by client and engagement type. The purpose is not to shame clients; it is to change terms, process or fit.

Finally, close the loop in sales. If a client requires long terms, the commercial owner sees the peak cash gap before pricing and approval. If a client repeatedly misses promises, renewal includes a new deposit, prepaid cadence or credit limit.

**Source notes:** Official MSME Samadhaan for delayed-payment information; Australian Government payment-terms guidance; AFP DSO definition; Atradius on billing errors. No benchmark is presented as universal.  
**CTA / funnel:** Inline CTA after chapter 2 to the free calculator; end CTA for an editable billing passport, reminder ladder and monthly scorecard. Beehiiv delivery with separate newsletter checkbox; tag `guide=agency-cash-collection`.  
**PDF/asset concept:** 18-page A4 workbook with contract-term worksheet, one-page billing passport, five-step reminder templates, dispute log, pause decision tree and monthly scorecard.  
**Visual briefs:** cash-collection swimlane; invoice approval route; escalation decision tree; DSO + overdue dashboard.  
**Internal links:** all ten articles, calculator, invoicing, contracts, CRM and agency partner page.

### Guide 2 — The Agency Milestone Billing Playbook

**Keyword / intent:** agency milestone billing / implementation.  
**Slug:** `/guides/agency-milestone-billing-playbook`  
**Meta title:** `Agency Milestone Billing Playbook`  
**Meta description:** `Design objective project milestones, approval windows, change orders and cash-safe invoice schedules.`  
**Editorial status:** Ready after legal review.

**Chapter structure:** 1) Map costs; 2) Choose deposit; 3) Define objective milestones; 4) Design approvals; 5) Handle changes; 6) Forecast delay; 7) Close and hand over.

#### Full guide copy

Milestone billing works when the commercial schedule mirrors the delivery risk. Begin with a cost map. Plot internal capacity, contractors, production, software and pass-through spend by date. The map reveals when the agency needs cash; percentages alone do not.

Choose a deposit that funds commitment. Ask what becomes irreversible at signature: capacity reservation, specialist booking, research or purchased media. The deposit should not be a random industry convention. Explain what it secures and when work begins.

Define each milestone with an observable event. “Design complete” is weak. “Client approves one selected visual direction from the agreed set” is better. State the approver, evidence, response window and what happens if feedback is late. Avoid placing most value behind final subjective approval.

Create a schedule table with milestone, planned date, percentage, invoice date, term, expected receipt and linked costs. Compare a base case with realistic delay. If the cumulative balance becomes negative, move a milestone, split it or prepay the related cost.

Connect changes to billing. Every change order states scope, price, timing, approval and payment trigger. The team does not start changed work because it appeared in chat. The client may approve, swap an existing item or defer it.

Control approvals. Send one review package, one decision request and one deadline. Consolidated feedback prevents a milestone from remaining half-approved. Record acceptance in the project system and trigger the invoice automatically, but keep a human owner for disputes.

At close, separate final payment from intellectual-property transfer or final handover only where the contract and advice support it. Deliver a clear closeout pack, archive approvals and review forecast versus actual receipt dates. Feed the variance into the next proposal.

**Source notes:** Government payment-terms guidance; Cora cash-gap methodology; existing Cora scope-creep material. The guide does not prescribe a universal deposit percentage.  
**CTA / funnel:** Embedded schedule preview sends users to the calculator. Lead magnet is an editable milestone schedule, approval matrix and change-order form. Beehiiv tag `guide=milestone-billing`.  
**PDF/asset concept:** 16-page field guide plus Google Sheets/Excel schedule with cash curve; workbook cells clearly label assumptions.  
**Visual briefs:** cost-to-cash timeline; strong vs weak milestone definitions; approval RACI; change-order flow.  
**Internal links:** Articles 1, 2, 6, 7 and 10; calculator; contracts.

### Guide 3 — The Late Payment Prevention & Recovery Playbook for Agencies

**Keyword / intent:** agency late payment process / urgent problem-solving.  
**Slug:** `/guides/agency-late-payment-playbook`  
**Meta title:** `Agency Late Payment Prevention & Recovery Playbook`  
**Meta description:** `Prevent avoidable invoice delays and use a calm, documented escalation process when agency payments become overdue.`  
**Editorial status:** Legal review required.

**Chapter structure:** 1) Prevent; 2) Detect; 3) Remind; 4) Resolve disputes; 5) Escalate; 6) Pause safely; 7) Learn and renew.

#### Full guide copy

The cheapest overdue invoice is the one the agency prevents. Prevention begins by selecting a fundable client and agreeing terms that match procurement reality. Confirm the legal entity, AP route, PO, approver, evidence and payment run before kickoff. Put the due date and dispute process in the contract and invoice.

Detect friction early. A portal rejection, missing PO or silent approver is not a minor administrative detail; it changes the expected receipt date. Track invoice accepted, due, promised, disputed and paid as separate states. Give each open receivable one owner.

Use a staged reminder sequence. Before due, verify readiness. On due date, restate the facts. A few days late, request a specific date. Later, involve the sponsor with a concise history and requested resolution. Never send daily automated pressure or continue a sequence after a reply, dispute or opt-out.

Treat disputes as cases. Record the client’s position, disputed amount, contract reference, delivery evidence, owner and next deadline. Separate the undisputed amount and ask whether it can be paid. Do not turn a genuine quality issue into a generic collections email.

Escalation is a business decision. Estimate the cost of continuing, the probability and timing of payment, dependency risks and relationship value. Check the contract and obtain advice for legal remedies. MSME delayed-payment mechanisms may apply to eligible Indian suppliers, but this guide cannot determine eligibility or outcome.

If work pauses, leave the project safe. Document what stops, what continues for security or compliance, how data and access are handled, and what restarts the work. Communicate once with authority; do not improvise threats.

After resolution, conduct a no-blame review. Was the invoice late, incorrect or disputed? Did the client miss a promise? Should terms, deposit, credit limit or account ownership change? Use the answer in renewal and future qualification.

**Source notes:** Official MSME Samadhaan; Australian Government payment-terms guidance; AFP and Atradius process notes. Legal and tax claims require India counsel before publication.  
**CTA / funnel:** Offer a downloadable reminder pack, dispute log and pause-work decision tree. Beehiiv tag `guide=late-payment`; sequence must not imply legal representation.  
**PDF/asset concept:** 20-page playbook with editable email scripts, evidence checklist, dispute case sheet, escalation matrix and post-mortem.  
**Visual briefs:** prevention funnel; receivable state machine; escalation ladder; safe-pause checklist.  
**Internal links:** Articles 3, 4, 8 and 9; calculator; contracts; offboarding.

## 4. Source register

1. Cora GA4, 18 September–17 October 2026: 226 sessions across returned landing pages, zero key events; `/partners/agencies` 19 sessions/18 engaged. Accessed 18 October 2026 via connected analytics.
2. Cora Search Console, same period: 112 query/page rows returned; no payment-terms, DSO, milestone-billing or collections queries. Accessed 18 October 2026.
3. [MSME Samadhaan](https://samadhaan.msme.gov.in/) — official delayed-payment monitoring portal; accessed 18 October 2026.
4. [Australian Government — Payment terms](https://business.gov.au/finance/payments-and-invoicing/payment-terms) — contract and invoice clarity; accessed 18 October 2026.
5. [Association for Financial Professionals — DSO](https://www.financialprofessionals.org/glossary/days-sales-outstanding-dso) — definition and interpretation; accessed 18 October 2026.
6. [Atradius — hidden cost of DSO](https://group.atradius.com/knowledge-and-research/resources/the-hidden-cost-of-days-sales-outstanding-dso) — invoicing accuracy and credit policy; accessed 18 October 2026.
7. [Cora pricing](https://heycora.in/pricing/) — Professional annual value ₹24,990; conflicting tax copy noted; accessed 18 October 2026.
8. Community research: current Reddit discussions surfaced recurring agency concerns about deposits, client-controlled approvals, continued work after overdue invoices and emotionally difficult follow-up. Community anecdotes shaped questions and UX, not quantitative claims.

## 5. Coding and editorial placement

Suggested repository placement after editorial approval:

- Tool PRD: `docs/product/free-tools/agency-invoice-cash-flow-calculator.md`
- Tool landing implementation: `app/tools/agency-invoice-cash-flow-calculator/`
- Articles: `content/articles/agency-finance/` and `content/articles/agency-operations/` using the slugs above.
- Guides: `content/guides/agency-cash-collection-playbook.md`, `agency-milestone-billing-playbook.md`, `agency-late-payment-playbook.md`.
- Lead assets: `public/downloads/agency-cash-collection/`.
- Analytics specification: `docs/analytics/agency-cash-gap-events.md`.

Recommended release order: calculator landing page and Article 1; Guide 1; Articles 2, 3, 6 and 8; Guides 2–3; remaining articles. Add bidirectional links at publication time. Do not publish Article 9 or the India-specific legal passages before review.

## 6. Daily growth report

- Produced: one complete free-tool PRD, ten publish-ready articles and three full playbooks with metadata, CTAs, internal links, sources and creative briefs.
- Handoff state: editorial package prepared; no tool built and no content published.
- Target cluster: agency payment terms, cash-flow gap, deposit vs milestone billing, DSO, collections, invoice approval, late payment and billing cadence.
- Funnel role: high-intent articles capture urgent finance/operations searches; the anonymous calculator creates product-qualified intent; three gated editable asset bundles grow Beehiiv with separate consent.
- Editorial blockers: legal review of MSME, pause-work and late-payment copy; resolve the Cora pricing page’s conflicting tax language before any tax-inclusive/exclusive claim.
