# ASSIGNMENT: Sampling and Reproducibility in Python

Read the blog post [Contact tracing can give a biased sample of COVID-19 cases](https://andrewwhitby.com/2020/11/24/contact-tracing-biased/) by Andrew Whitby to understand the context and motivation behind the simulation model we will be examining.

Examine the code in `whitby_covid_tracing.py`. Identify all stages at which sampling is occurring in the model. Describe in words the sampling procedure, referencing the functions used, sample size, sampling frame, any underlying distributions involved, and how these relate to the procedure outlined in the blog post.

Run the Python script file called whitby_covid_tracing.py as is and compare the results to the graphs in the original blog post. Does this code appear to reproduce the graphs from the original blog post?

Modify the number of repetitions in the simulation to 1000 (from the original 50000). Run the script multiple times and observe the outputted graphs. Comment on the reproducibility of the results.

Alter the code so that it is reproducible. Describe the changes you made to the code and how they affected the reproducibility of the script file. The output does not need to match Whitby’s original blogpost/graphs, it just needs to produce the same output when run multiple times

# Author: ADRIENNE LLOREN

```
Please write your explanation here...

```

### Examination of the Code
The whitby_covid_tracing.py script simulates the process of COVID-19 infections and contact tracing for individuals attending events, specifically weddings and brunches.

#### Sample Frame
The sample frame consists of 1000 people in the community. These individuals are distributed across different events:

* Weddings: 2 weddings with 100 attendees each.
* Brunches: 80 brunches with 10 attendees each.

#### Sample Size
The sample size can be understood at different stages:

* Total Population: 1000 individuals.
* Attendees at Events:
    * Weddings: 2 events × 100 attendees = 200 people.
    * Brunches: 80 events × 10 attendees = 800 people.
* Infected Individuals:
    * Each individual has a 10% chance of being infected, so the expected number of infections varies due to the randomness in the simulation.

#### Sampling Procedure
The sampling procedure in this model consists of three steps:

1. Simulating Infections:

    * Function: simulate_event(n_events, n_attendees, infection_rate)
    *  Description: This function uses a binomial distribution to simulate the number of infections at each event. Each individual at an event has a 10% chance of being infected.

2. Primary Contact Tracing:

    * Function: trace_infections(n_events, infections, trace_prob)
    * Description: This function simulates tracing infections back to their events. Each infection has a 20% chance of being traced. This means that out of all infected individuals, only 20% are likely to be identified as linked to a particular event.

3. Secondary Contact Tracing:

    * Description: If at least two infections are traced back to the same event, all infections from that event are identified. This step ensures that if multiple cases are found from the same event, a thorough follow-up detects all associated infections.

#### Analysis of Bias in Contact Tracing
The blog post discusses how contact tracing can lead to biased samples because some events are easier to trace than others. In the model:

* Weddings: Easier to trace due to more attendees and higher chances of identifying multiple infections. Weddings often have guest lists and contact information collected by the event planner.
* Brunches: Harder to trace due to fewer attendees per event and fewer chances of identifying multiple infections. Identifying individuals who attended brunches is harder because restaurants typically do not gather contact information from patrons unless reservations are made.

This results in an overestimation of infections from easily traceable events (like weddings) and an underestimation from harder-to-trace events (like brunches). Understanding the steps in the sampling procedure and their rationale helps appreciate the model's demonstration of bias in contact tracing.

#### Comparing Graph Results
Original Blog Post Graph:
Proportion of infections resulting from weddings peaks between 0.18 and 0.23 (18% to 23%) and has a spread between 0.08 and 0.35 (8% to 35%).

Simulation Results:
When the code is run with 50000 repetitions, the proportion of infections resulting from weddings peaks between 0.15 and 0.20 (15% to 20%) and has a spread between 0.06 and 0.35 (6% to 35%).
These numbers are slightly off but still similar in shape.

The observed proportion illustrated in the blog post differs from the output of the whitby_covid_tracing.py code. The blog post shows a larger spread (0.03 to 0.08, or 30% to 80%) than the simulation results. Therefore, the code reproduces similar results for "infections from weddings" but does not fully match the blog post's results.

#### Reproducibility of Results
Modification: Changing the number of repetitions in the simulation to 1000 (from the original 50000) and running the code multiple times.

Observation: The output graphs varied slightly each time, indicating that their spread and peaks were not exactly the same but still quite similar.
To make the results reproducible, I made the following changes:

Set a Random Seed: Added a random seed (np.random.seed(42)) to ensure consistent results.

Created a Function: Developed a run_simulation function to set the random seed and repetition when running the simulation.
After these modifications, I was able to reproduce the same results consistently. The test code in test_runs.ipynb shows these simulations.

## Criteria

|Criteria|Complete|Incomplete|
|--------|----|----|
|Altercation of the code|The code changes made, made it reproducible.|The code is still not reproducible.|
|Description of changes|The author explained the reasonings for the changes made well.|The author did not explain the reasonings for the changes made well.|

## Submission Information

🚨 **Please review our [Assignment Submission Guide](https://github.com/UofT-DSI/onboarding/blob/main/onboarding_documents/submissions.md)** 🚨 for detailed instructions on how to format, branch, and submit your work. Following these guidelines is crucial for your submissions to be evaluated correctly.

### Submission Parameters:
* Submission Due Date: `HH:MM AM/PM - DD/MM/YYYY`
* The branch name for your repo should be: `sampling-and-reproducibility`
* What to submit for this assignment:
    * This markdown file (sampling_and_reproducibility.md) should be populated.
    * The `whitby_covid_tracing.py` should be changed.
* What the pull request link should look like for this assignment: `https://github.com/<your_github_username>/sampling/pull/<pr_id>`
    * Open a private window in your browser. Copy and paste the link to your pull request into the address bar. Make sure you can see your pull request properly. This helps the technical facilitator and learning support staff review your submission easily.

Checklist:
- [x] Create a branch called `sampling-and-reproducibility`.
- [x] Ensure that the repository is public.
- [x] Review [the PR description guidelines](https://github.com/UofT-DSI/onboarding/blob/main/onboarding_documents/submissions.md#guidelines-for-pull-request-descriptions) and adhere to them.
- [x] Verify that the link is accessible in a private browser window.

If you encounter any difficulties or have questions, please don't hesitate to reach out to our team via our Slack at `#cohort-3-help`. Our Technical Facilitators and Learning Support staff are here to help you navigate any challenges.
