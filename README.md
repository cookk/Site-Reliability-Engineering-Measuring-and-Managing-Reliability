## About this course
## What is SRE? How does it differ from DevOps?
## Who are CREs? How they can help you be more reliable?
## Why are SLOs important for your organization?
## Introduction: Targeting Reliability
- What to promise to whom
- What metrics to measure
- How much reliability is good enough
## Promises, Promises. SLOs vs. SLAs. Happiness Test.
- SLA
  - Violating SLAs requires costly compensation.
- SLO
  - They should always be stronger than your SLAs because customers are usually impacted before the SLA is actually breached.
  - An SLO is effectively an internal promise to meet customer expectations.
  - When you meet your target SLOs, users are happy. When we miss target SLOs, users are sad.
- Happiness Test
  - The test states that services need target SLOs that capture the performance and availability levels that if barely met would keep a typical customer happy.
  - The challenge is quantifying and measuring the happiness of your customers since you can't do this directly.
  - You have to be able to make sure you're thinking about all groups of your customers.
## How do we measure reliability? Edge cases.
- Measuring Reliability
  - Time to start playing(=latency)
  - No interruptions or issues with playback
- SLI(Service Level Indicators)
  - (good events / valid events)
  - ex)
    - request latency
    - Error rate = ratio of erros or successes/total requests
    - Error rate = erros or successes/throughput
  - pros, cons, tradeoffs
    - For example, perhaps you're already exporting the data for your SLI to your monitoring system, which is a big plus. But maybe it's not saving history far back enough, or you've come with a perfect measure of user experience but actually implementing that measurement is way too complex.
  - How do you set SLOs for SLIs?
- Edge cases
  - The impact of outages isn't always constant over time.
    - ex) Balck Friday
      - they might shift from wanting a three nines available service for most of the year to something closer to four nines, which they address by temporary strategies, such as over-provisioning resources, implementing change freezes, or utilizing war rooms.
    - ex) Outage duration can impact customer
    happiness
      - 4 one-hour outages vs. 1 four-hour outage vs. constant 0.5% errors.
  -  It's common to set a target for the median user and for the long tail to make sure that it doesn't get too long.
## How reliable shoud a service be? Setting targets for reliability. Iterate!
- 100% is the wrong target
> "100% is the wrong reliability target for basically everything."  - Ben Treynor, Google, LLC
  - Higher availability costs you more to provide, reducing your ability to make changes and release new features.
  - If you want to improve reliability, sooner or later, you're going to need to slow down changes by having things like increased testing, less frequent releases and more manual analysis.
- Iterating
  - Running a service with an SLO is an adaptive and iterative process.
  - You should expect to regularly re-evaluate the details of your chosen SLIs and the SLO targets you put on.
## Introduction: Operating for Reliability
- Learn how to...
  - Quantify missed reliability targets with error budgets.
  - Make business decisions based on reliability targets.
  - Make a service more reliable.
## When do we need to make a service more reliable? Error budgets.
- Error budgets
  - Inverse of avaiability.
  - How your service is allowed to be.
  - 99.9% success(SLO) = 0.1% failure(error budget) = 40.32 minutes of downtime per month(28 days).
  - Benefits
    - Common incentives for Devs and SREs
    - Dev team can self-manage risk
    - Unrealistic goals become unattractive
## Trading off reliability against features
- Everything is trade-off
  - When you try to maximize your reliability, you're limiting development velocity of new features, quicker releases, etc.
  - Align Incentives
    - Devs can take risks and push more quickly.
    - SRE team can work more proactively.
  - Reliability vs. ($$Cost$$, Velocity)
  - Effective SLOs
    - Have executive buy-in.
    - Have consequences.
    - Are accurately measured.
- Advanced Techniques
  - Dynamic release cadence
    - Based on remaining error budget
  - "Rainy Day" Fund
    - Covers unexpected events
  - Error budget-based alerts
    - Exhaustion rate drives alerting
  - "Silver bullets"
    - For "critical" new features
    - Silver bullets aren't required to fix latency, quality or reliability problems that are causing a negative user experience.
    - Silver bullets do not roll over.
    - The use of a silver bullet is generally regarded as a failure, and it should trigger a post mortem or other retrospective to learn what went wrong and how to fix it for next time.
> Excessive helpfulness is harmful.
## How do we make a service more reliable?
- Axes of improvement
  - TTD: time-to-detect
  - TTR: time-to-repair or time-to-resolution
  - Improve reliability by
    - Reducing detection time: lower TTD
    - Reducing repair time: lower TTR
    - Reducing impact %: Canary deployment
    - Reducing frequency: higher TTF
- Operational approach to increasing reliability
  - Report on uneven error budget spend
  - Provide input on achieving targets
  - Standardize Infrastructure
  - Consult on system design
  - Build safe release and rollback
  - Author postmortems
  - Use phased rollouts
- **Module summary**
  - **Define your problem space: SLOs and SLIs.**
  - **Make your system as reliable as it must be, but no more.**
  - **Error budgets are your primary basis of communication.**
  - **SLOs are not set in stone forever.**
  - **The team relationship has to be strong to make this work.**
## Introduction: Choosing a Good SLI
- Learn how to...
  - Choose the right metric.
  - Measure your SLIs.
  - Choose an SLI specification.
  - Refine an SLI implementation.
  - Reduce SLI complexity.
  - Set SLO targets.
## Metrics and Measurement
- User happiness in metric form
  - Ideally, you wanted to define SLIs that have a predictable, mostly linear relationship with happiness of your users.
- The properties of good SLI metrics
  - (X) System metrics(load average, CPU utilization, memory usage, bandwidth ..)
    - Users don't directly see your CPUs pegged at 100 percent.
    - They see your service responding slowly.
  - (X) Internal state(thread pool fullness, request queue length ..)
    - The data is noisy, and there are many reasons why large changes could occur.
  - (V) Has predictable relationship with user haapiness.
  - (V) Shows service is working as users expect it to.
  - (V) Expressed as: (good events) / (valid events)
  - (V) Aggregated over a long time horizon.
    - We suggest that the SLI be aggregated over a reasonably long time window, to smooth out noise from the underlying data.
    ![image1](https://github.com/cookk/Site-Reliability-Engineering-Measuring-and-Managing-Reliability/blob/master/the_properties_of_good_sli_metrics_1.PNG)
