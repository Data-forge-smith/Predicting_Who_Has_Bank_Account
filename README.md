# Predicting_Who_Has_Bank_Account

*A data science case study: using survey data to help close the financial inclusion gap in Africa.*

**The business problem**

Having a bank account has long been treated as a core measure of financial inclusion. Even with the rapid spread of mobile money and new fintech services, banks remain central to bringing people into the financial system. An account lets households save and make payments, and helps small businesses build a credit record that opens the door to loans and insurance. That makes account access an important driver of long-term economic growth.

Yet in many African countries a large share of adults still has no account. Banks, mobile money providers, governments and development organisations all want to change that, but they have limited budgets and cannot reach everyone at once.

The question I set out to answer: based on a few simple facts about a person, can we predict whether they have a bank account, so that outreach can be aimed at the people who need it most?

This project was built for the Zindi Financial Inclusion in Africa challenge. It asks for a model that predicts who is most likely to have or use a bank account in Kenya, Rwanda, Tanzania and Uganda, and that sheds light on the factors behind people's financial security.

**The data**

The data comes from household surveys and covers 23,524 people across Kenya, Rwanda, Tanzania and Uganda. For each person it records where they live (country, and whether the area is rural or urban), whether they have access to a mobile phone, and who they are: age, gender, household size, relationship to the head of the household, marital status, education level and type of work.

The survey also records whether each person has a bank account, which is what the model learns to predict. Nothing that identifies an individual was used. I removed each person's ID before modelling.

**My approach, in plain terms**

1. Prepared the data so a computer could learn from it. Yes/No and rural/urban answers became simple 1s and 0s, and categories such as education level and job type were converted into a form the model can use.
2. Held back 30% of people as an exam. The model never saw them while learning, so its score on them reflects how it would do on new people.
3. Rebalanced the learning data. Fewer people have accounts than don't, and a model can ignore the smaller group if left alone. I created realistic extra examples of account holders for training only by resampling using SMOTENC, never for the exam.
4. Built the whole process as one reusable pipeline. Preparation, rebalancing and prediction run together as a single unit. This keeps the exam honest, because nothing from the exam group leaks into training, and it means the same process can be re-run on new survey data without manual steps.
5. Tested many settings automatically to find the best configuration of the model.
6. Chose the decision cut-off carefully. The model gives each person a likelihood of having an account. I tested a range of cut-off points for turning that likelihood into a yes or no, and picked the one that made the fewest mistakes.
7. Retrained on all the available data before predicting for the competition's unseen test set, and produced a submission file in the required format.

**What I found**

I tried different settings on the model and the result provided
1. Standard settings - 87.4%
2. After automatic tuning - 87.7%
3. After choosing the best cut-off - 88.5%

Two lessons stand out:

1. Gains were small and steady, not dramatic. Tuning the model added a fraction of a point. Choosing the right cut-off added about a full point, more than the tuning did. Simple decisions can matter more than complicated ones.
2. A well-built process matters as much as the model itself. Keeping the rebalancing inside the training step gives a trustworthy estimate of real-world performance, rather than an inflated one.

**How this could be used**

1. Targeting outreach. Direct awareness campaigns, agent networks or mobile banking offers at the groups least likely to have an account.
2. Planning where to expand. See which combinations of location, education and work type are most underserved before opening new branches or agents.
3. Tracking progress. Re-run the same pipeline on new survey rounds to see whether the gap is closing.

**Limitations of model**

1. Overall accuracy does not tell the whole story. Because fewer people have accounts than don't, a high score can hide weaker performance on the smaller group. The next step is to report how many actual account holders the model finds, and how many of its flags are correct.
2. It shows who is likely to be unbanked, not why. Reasons such as cost, distance, trust or documentation need separate research.
3. Personal characteristics such as gender and age are inputs. Any real use should aim to widen access, never to deny service to anyone, and should be checked for fairness across groups.
4. The data is a survey snapshot. Results should be re-checked as people's circumstances and mobile technology change.

**Skills demonstrated**

Framing a social and business problem as a prediction task, preparing mixed survey data, handling uneven groups without distorting the results, building a leak-free reusable pipeline, tuning and threshold selection, producing a competition submission, and explaining the work in plain language.
