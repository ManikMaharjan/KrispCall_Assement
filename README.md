 
KrispCall Revenue Attribution Analysis — Final Summary
Why we did this
We wanted to figure out which integration platforms bring in the most revenue for KrispCall.
To do that, we looked at things from three angles:
1.	First-Touch Attribution – Gives all the credit to the first integration a customer connected after they started paying.
2.	Usage-Based Attribution – Spreads the credit based on how much the customer actually used each platform (calls + SMS).
3.	Position-Based Attribution – A hybrid that gives weight to both the first and last integrations, with a little credit to anything in between.
We used four main datasets:
•	Workspace data – which users belong to which paying account.
•	Payments and refunds – so we know exactly how much net revenue each account brought in.
•	Integration events – when a user connected or disconnected a platform.
•	Call/SMS usage data – how much activity happened and when.
 
How the data was prepared
We started by expanding each workspace to include every user in it (owners + members). That way, even if the activity came from a team member, we could still link it to the paying account.
For payments and refunds:
•	We matched them by account owner.
•	We calculated net revenue = (total payments) − (total refunds).
•	We only kept accounts where net revenue was positive — because there’s nothing to attribute if the account brought in no money.
For integration events:
•	We matched “connected” events to the next “disconnected” event to find connection windows for each platform.
•	If no disconnect was found, we assumed the connection stayed active until a refund date (or still active if no refund).
For call/SMS usage:
•	We converted call times from strings like "431.0 seconds" into numbers.
•	We converted SMS segments into seconds using 1 segment = 5 seconds (this can be changed later to test sensitivity).
•	We added these together to get total usage units for each platform.
We made sure:
1.	Usage had to happen after the first payment and before any refund.
2.	Usage only counted if the platform was connected at that time (except web and mobile, which are always available).
3.	Every user in the integration/usage data matched to an account in the workspace list.
 
How the three attribution models worked
1.	First-Touch
For each paying account, we found the very first integration connected after their first payment.
All of their revenue goes to that one platform.
If they never connected anything, they went into a “No Integration” bucket.
2.	Usage-Based
For each account, we looked at how much total usage happened on each platform.
Then we gave each platform a share of that account’s revenue based on its share of the usage.
If an account had no recorded usage, their revenue went into a “No Usage” bucket.
3.	Position-Based (Chosen model for main insights)
o	1 platform → gets 100% of the revenue.
o	2 platforms → first gets 60%, last gets 40%.
o	More than 2 → first gets 40%, last gets 40%, middle platforms split the remaining 20%.
This way, we give importance to both the platform that started the relationship and the one they ended up with most recently.
 
What we found
The three models give very different pictures:
•	First-Touch often highlights platforms that are strong in acquisition — the ones customers connect first.
•	Usage-Based rewards platforms where the most calls and SMS actually happen — often web and mobile perform strongly here.
•	Position-Based balances both sides, showing platforms that matter at both the start and the ongoing usage stages.
We also saw a chunk of accounts with “No Integration” or “No Usage” — meaning either they didn’t connect any integrations, their usage wasn’t captured, or they churned early.
 
What to do with this information
1.	For marketing & partnerships:
Use the First-Touch winners to decide where to focus acquisition efforts — these are the channels that bring people in.
2.	For product investment:
Focus on Usage-Based top performers — these are where customers are most active and therefore most valuable in retention terms.
3.	For customer experience:
Look at Position-Based leaders — they often influence both acquisition and retention.
4.	For data & operations:
Investigate the “No Usage” and “No Integration” buckets — find out if it’s a tracking issue or a customer problem.

 
Files produced
•	first_touch_attribution.csv – Revenue by platform under the first-touch model.
•	usage_based_attribution.csv – Revenue by platform based on usage share.
•	chosen_attribution.csv – Revenue by platform under the position-based model.
•	analysis_summary.txt – This report.
•	attribution_analysis.py – The full code so the process can be repeated.

<img width="468" height="662" alt="image" src="https://github.com/user-attachments/assets/514fabd8-db5b-4647-abcb-7d80d39cfb8f" />
