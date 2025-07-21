# Buffer Fever Chart for Jira (Cloud)
### What is it?
This Power BI template is designed for teams using Jira (Cloud) who want to move beyond surface-level metrics and gain deeper insights into delivery health. It focuses on flow-based indicators rather than traditional measures like velocity. The core visual, the *Buffer Fever Chart*, is a tool that is used extensively in [TameFlow](https://tameflow.com/) and in Critical Chain Project Management (CCPM) used in the Theory of Constraints.

### Prerequisites
* [Make sure you have the latest version of Power BI Desktop](https://aka.ms/pbiSingleInstaller)
* [Follow these steps](https://support.atlassian.com/atlassian-account/docs/manage-api-tokens-for-your-atlassian-account/) to setup a Jira API token and note it down (e.g. copy/paste into Notepad)
* [Download the template file](https://github.com/nbrown02/BufferFeverChart/raw/refs/heads/main/Buffer%20Fever%20Chart%20(Jira).pbit)
* Then you're good to get started!
* Please note: I don’t store, use or have access to any of your data/information. It’s all within your machines/network :)

### Connectivity
* Open the .pbit file in Power BI Desktop
* Add your Jira URL 
* Add your Jira Project Key (ensure this is capitalised!)

Don't confuse the project name with the project key, a common mistake! Your project key will be in the URL when viewing an item.

* It should then look something like this:
  
![alt text](https://raw.githubusercontent.com/nbrown02/BufferFeverChart/refs/heads/main/Screenshot3.png)

* Hit 'Load' 
* You will be prompted for a login, choose Basic and enter:
  - Your email associated with your Jira account for your username
  - Your API token you created in the Prerequisities

![alt text](https://raw.githubusercontent.com/nbrown02/FlowViz-Jira/main/Screenshots/Login2.png)

* Then hit 'Connect' and wait for the data and charts to load!

### What do these charts mean? How can I learn more?
For an introduction about the topic, read:
- [Critical Chain Project Management in the Theory of Constraints](https://tameflow.com/blog/2012-09-25/critical-chain-project-management-in-TOC/)
- [Buffer Management and Risk Management in Theory of Constraints](https://tameflow.com/blog/2012-10-04/buffer-management-and-risk-management-in-TOC)
- [Visual Portfolio Management](https://tameflow.com/blog/2014-11-25/visual-portfolio-management)
- [How to Draw Buffer Fever Charts](https://tameflow.com/blog/2017-03-30/how-to-draw-buffer-fever-charts/)

### Screenshots

![alt text](https://raw.githubusercontent.com/nbrown02/BufferFeverChart/refs/heads/main/Screenshot1.png)

![alt text](https://raw.githubusercontent.com/nbrown02/BufferFeverChart/refs/heads/main/Screenshot2.png)

### Assumptions, calculation and shortcomings behind the template
#### Assumptions 
- All Epics and their respective child items (typically Stories) are located in the same Jira project.
- Your Jira workflow configuration correctly maps issue statuses to the standard status categories: To Do, In Progress, and Done.
- Each day's snapshot reflects the current state of each epic's child items on that date. Epics are assumed to progress over time via incremental status updates.
- Epics are owned by an individual team (i.e. not shared)

#### Calculations/Logic
- %Completed is based on the proportion of child items in the "Done" status category, calculated relative to the total (Done + In Progress + To Do).
- Buffer size is derived from the difference between the 85th and 50th percentile *story-level* cycle times, multiplied by the epic's initial scope (child item count on day 1).
- Expected time is calculated by multiplying the % completed by the 50th percentile story cycle time, then scaled to the epic’s initial scope.
- Buffer consumed is the time elapsed minus expected time, divided by the buffer size. It is clamped between 0% and 100% to simplify interpretation.
- Trajectory over time (e.g. Today / 1 week ago / 2 weeks ago) is calculated using the current epic status at that point in time. These are displayed as overlapping dots of descending size to help visualize progress or stalling.
- Forecasting logic is driven by average throughput (stories completed per day), used to project epic end dates based on remaining work.
- Only items completed in the last 16 weeks are included in Throughput/Cycle Time (Story level) - just to aid performance and data load times

#### Shortcomings
- Snapshots only reflect the data available for that day — if epics have no activity or missing story states on a given date, it may misrepresent true progress.
- If child items are added or removed mid-flight, the buffer and expected time calculations may lose some accuracy unless carefully interpreted.
- Assumes each child item carries equal weight; there's no adjustment for item size, complexity, or effort.
- Outliers in story cycle times can skew the 85th percentile and inflate buffer sizes unless manually adjusted.
- Forecasting assumes a constant throughput rate and does not account for planned pauses, dependencies, or resource shifts.
- Power BI doesn't allow for the background RAG mapping directly in the charts, so it is a static background image that may be slightly off - it as close to the scale/logic [documented here](https://tameflow.com/blog/2017-03-30/how-to-draw-buffer-fever-charts/) as possible
- This doesn't filter by team, if you have multiple teams within a Jira project you will need to modify the queries yourself to account for this

### Feedback
This template is built and maintained by [Nicolas Brown](https://www.nicolasbrown.co.uk/) in collaboration with [Steve Tendon](https://tameflow.com/) - reach out to either of us with your feedback.
