**SENG 637- Dependability and Reliability of Software Systems***

**Lab. Report \#5 – Software Reliability Assessment**

| Group: 14      |
|-----------------|
| Ayodele Oluwabusola        |   
| Gabriel Gabari             |   
| Remi Oyediji               |   
| Taiwo Oyewole              | 

# Introduction
In this lab report, our group analyzed failure data from a hypothetical system using two key methods: Reliability Growth Testing and the Reliability Demonstration Chart (RDC). These methods helped us understand how system reliability changes and improves during testing. 
We used "C-SFRAT" to track failure rates and reliability over time. Since the tool didn’t run properly on the Windows 10 PC that we used, we successfully ran it using **Oracle VM VirtualBox**. This hands-on experience helped us see the importance of reliability testing in real-world scenarios and better understand the tools used in the process.

We explore two main techniques for assessing system reliability: Reliability Growth Testing and the Reliability Demonstration Chart (RDC). These methods help us evaluate the overall quality and dependability of the System Under Test (SUT) using the provided failure data.
Here's how we broke it down:

1. Techniques used:
   - Reliability Growth Testing
   - Reliability Demonstration Chart (RDC)

2. What we analyzed:
   - How long the system ran (T)
   - How many failures were found (FC)
   - Time spent running tests (E)
   - Human effort to detect bugs (F)
   - Computer time used (C)

3. What we aimed to learn:
   - How the system’s reliability improves
   - How failure trends can guide decisions

These methods gave us insight into how reliable the system is and what areas may need more attention.


# Assessment Using Reliability Growth Testing 

### **2.1 Result of Model Comparison**

We used C-SFRAT to estimate failure trends across all available models and covariate combinations. The goal was to identify the two models that best fit the observed failure data. We evaluated each model based on **Akaike Information Criterion (AIC)** and **Bayesian Information Criterion (BIC)**. They indicate a better balance between model fit and complexity:

- **AIC (Akaike Information Criterion)**: Penalizes complexity mildly. Lower AIC means a better fit with fewer parameters.
- **BIC (Bayesian Information Criterion)**: Penalizes complexity more strongly. Lower BIC indicates a simpler, more generalizable model.

The top-performing models were:

- **Discrete Weibull Type III with covariate F** - best AIC and BIC.
- **Geometric with covariate F** - second best in both metrics.
- 
Below is a snapshot of the comparison result from the tool. Highlighting the best two models with the lowest AIC and BIC metrics.

<img src="media/1-Comparison for all models.png" alt="media/1-Comparison for all models.png" >

*Figure 1: Table showing models' comparison*

<img src="media/2-model results and prediction.png" alt="media/2-model results and prediction.png" >

The figure displays simulations using all models and covariate combinations, illustrating cumulative failures from the imported data. Models were run with no covariates (None) or combinations (E, F, C).


### **2.2 Result of Range Analysis**

We applied the **Laplace trend test** to determine the time interval range where failure intensity showed reliability growth (i.e., decreasing failures).

- The Laplace factor was **negative from interval 1 to 19**, indicating improving reliability.
- However, we extended the range to **interval 1 to 21**, even though intervals 20 and 21 had near-zero Laplace values. Including them improved model accuracy without introducing noise.

This range (1–21) gave the most stable and insightful prediction window.

**Insert Image**: *Line plot of Laplace factor across intervals — highlight transition from negative to near-zero around interval 19–21.*

---

### **2.3 Plots for Failure Rate and Reliability of the SUT**

Using the selected models (DW3(F), GM(F)) and the 21-point range, we plotted:

- **Cumulative Failure (MVF)**: shows total expected failures over time.
- **Failure Intensity**: shows how fast failures are occurring at each point.

After tuning covariate **F = 20**, both models aligned well with actual failure trends, especially at later intervals where failure rate spiked.

**Insert Image 1**: *MVF (Cumulative Failure) plot comparing actual data vs. DW3(F) and GM(F).*

**Insert Image 2**: *Failure Intensity plot showing how each model captures the sudden increase in failure rate.*


### **2.4 Decision Making with Target Failure Rate (5 marks)**

We tested model predictions by setting failure intensity targets:

- **Target = 0.3**:
  - **GM(F)**: Needs **59 more intervals**.
  - **DW3(F)**: Already meets the target — needs **0 intervals**.

- **Target = 2.5**:
  - **GM(F)**: Needs **5 more intervals**.
  - **DW3(F)**: Needs **6 more intervals**.

**Interpretation**: DW3(F) is more aggressive and reaches reliability targets faster. GM(F) is more conservative but stable.

**Insert Image**: *Two side-by-side bar charts or line graphs for model response to target failure rates 0.3 and 2.5.*




### 2.5 Advantages and Disadvantages of Reliability Growth Analysis

 **Advantages**

1. **Spotting Problems Early**: 
   Reliability growth analysis helps catch issues early in the testing phase. By watching how failures trend, we can fix problems before they turn into bigger ones, ultimately improving the system’s performance.

2. **Better Predictions**: 
   This analysis helps predict how reliable the system will be over time. With this info, it’s easier to plan resources and manage risks, ensuring that the system stays reliable as it moves through different stages.

3. **Helps Design Decisions**: 
   The insights from the analysis can guide engineers on which parts of the system need more work. It makes sure that we’re focusing on the areas that will have the biggest impact on reliability.

4. **Data-Driven**: 
   Since this analysis is based on actual failure data, it gives us something solid to rely on when making decisions, instead of just guessing or assuming things about how the system will behave.

**Disadvantages**

1. **Picking the Right Model**: 
   Choosing the right model for the analysis can be tricky. Not all systems are the same, and using the wrong model might give us misleading results. You need to really understand the system to pick the right one.

2. **Need for Lots of Data**: 
   Reliability growth analysis works best with a lot of failure data over time. But if you’re working with a new system or one that hasn’t been tested enough, it can be tough to get enough data, making the analysis less useful.

3. **Assumptions Can Be Off**: 
   Many models make assumptions about how failures should behave, but these don’t always match up with real-world situations. This means the predictions might not always be accurate if the assumptions don’t fit the actual failure patterns.

4. **Time-Consuming**: 
   Running the analysis, especially when you have a lot of intervals or complex models, can take a long time. If you’re in a rush and need quick decisions, it might not be the most efficient method to use.

# Assessment Using Reliability Demonstration Chart 

# 

# Comparison of Results

# Discussion on Similarity and Differences of the Two Techniques

# How the team work/effort was divided and managed

# 

# Difficulties encountered, challenges overcome, and lessons learned

# Comments/feedback on the lab itself



Here's a detailed yet concise write-up that incorporates the necessary elements from the provided texts, focusing on reliability growth testing, model comparison, analysis, and decision-making. I’ve indicated where the plots should be placed and referenced specific images based on the experiment.

---

### 2. **Assessment Using Reliability Growth Testing**

In this section, we assess the reliability of the System Under Test (SUT) using **reliability growth testing** (RGT). This method helps us understand how the reliability of the system evolves over time, taking into account detected failures and model predictions. The data consists of **time intervals**, **failure counts**, and **execution time** for each interval, alongside **effort** and **computer time** required to identify failures. Using the C-SFRAT tool, we ran reliability estimations across several models with different covariate combinations.

#### **Result of Model Comparison (Selecting Top Two Models)**

We compared all available models based on their **Akaike Information Criterion (AIC)** and **Bayesian Information Criterion (BIC)** values. Both metrics help determine the best-fit models, balancing model complexity and accuracy. The models considered include **Discrete Weibull (DW3)**, **Geometric (GM)**, and others. After sorting the models by AIC and BIC, the top two models chosen were **DW3(F)** and **GM(F)**.

- **Figure 1**: *Reliability growth modeling across all models and covariate combinations* (shows simulation using all models and covariates, highlighting cumulative failures).
  
- **Figure 2**: *Best two models with lowest AIC and BIC metrics* (shows the top two models: DW3(F) and GM(F)).

#### **Result of Range Analysis**

To refine our analysis, we applied the **Laplace range analysis** to identify the most effective data subset for reliable predictions. The analysis showed that the reliability improves between the **2nd and 18th intervals**, but decreases after the **19th interval**. A range of **0 to 21** intervals was selected for further analysis, as it provided a better prediction without omitting important failure patterns.

- **Figure 3**: *Laplace range analysis plot* (shows reliability fluctuations between intervals, highlighting the optimal data range).

#### **Plots for Failure Rate and Reliability of the SUT**

Next, we examined the **failure intensity** (rate of failures) and **reliability** using the selected models. These plots help visualize how the failure rate changes over time, providing insight into system performance under test.

- **Figure 4**: *Failure intensity plot using all data* (shows failure rate over time based on all available data).
  
- **Figure 5**: *Failure intensity plot using subset of 21 data points* (focuses on predictions based on the selected subset, showing reduced noise and better trend analysis).

- **Figure 6**: *Reliability plot for both DW3(F) and GM(F)* (shows cumulative failure predictions over time).

#### **Discussion on Decision-Making Given a Target Failure Rate**

In real-world applications, companies set acceptable **failure rates** (e.g., 2 failures/interval). By comparing our model predictions with target rates, we can determine if the system meets these standards. For example:

- **Example 1**: If the acceptable failure rate is **2 failures/interval**, the system would be deemed unacceptable at the **31st interval**, as the observed failure rate is **2.96**.
  
- **Example 2**: If the acceptable failure rate is **3 failures/interval**, the system remains acceptable at the **31st interval**. However, the **DW3(F)** and **GM(F)** models predict that this rate might exceed the acceptable threshold in the future, allowing proactive adjustments.

- **Figure 7**: *Decision-making plot* (illustrates how failure rate predictions align with different target failure rates over time).

---

### Conclusion

The reliability growth testing, model comparison, and failure rate analysis provide a clear picture of the SUT's performance. By focusing on the top-performing models (DW3(F) and GM(F)), we can make informed decisions about system reliability and target failure rates. The use of **range analysis** and **failure intensity plots** helps refine predictions, ensuring better reliability forecasting.

---

This structure directly addresses the key sections of the assignment, with images placed where relevant to visually support the findings and analysis. Let me know if you'd like any further adjustments!
