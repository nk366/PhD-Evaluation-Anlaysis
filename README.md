# PhD-Evaluation-Anlaysis

## Surfwell Study 2: quantitative analysis pipeline TP1,4,5

R and Quarto code for the quantitative analysis in Study 2 of a realist evaluation of Surfwell, a surf therapy programme for UK emergency service workers. The work forms part of a PhD at the University of Exeter, funded by the ESRC.

The pipeline takes the raw survey exports from three timepoints and produces cleaned and scored data, descriptive tables, statistical tests with multiple-testing correction, Reliable Change Index (RCI) classifications and figures.

### Timepoints

Label	Meaning
TP1	1-Week Before the programme
TP4	2-Week Follow-Up
TP5	3-Month Follow-Up
Version: V1.1
Archived copy with DOI: NA yet



## Stage	What it does	Reads	Writes
1	Cleans the raw Qualtrics exports	data/raw/tp1_final.xlsx, tp4_final.xlsx, tp5_final.xlsx	data/clean/cleaned_tp1.rds, cleaned_tp4.rds, cleaned_tp5.rds
2	Renames columns and merges the timepoints	cleaned_tp*.rds	data/clean/merged_data.rds, program_theory.xlsx
3	Recodes text responses to numbers	merged_data.rds	data/clean/recoded_data.rds
4a	Scores each measure	recoded_data.rds	data/clean/scored_data.rds
4b	Attrition, participant characteristics and mental health summary tables	scored_data.rds, cleaned_tp*.rds	data/analysis/participant_characteristics_TP1_TP4_TP5.xlsx
4c	Groups and labels for each measure (lookup)	none	data/analysis/measure_groups.rdata
5	Descriptives, tests, Bonferroni correction and RCI	scored_data.rds, measure_groups.rdata	data/analysis/analysis_results.rdata, test_results_summary.xlsx
6	Bar charts and RCI scatter plots	analysis_results.rdata, measure_groups.rdata	figures in data/analysis/
7	Programme theory bar chart	data/clean/program_theory.xlsx	figure in data/analysis/
8	RCI stacked-bar figures	analysis_results.rdata, measure_groups.rdata	figures in data/analysis/
9	Package citations and session record	the .qmd file (as text)	data/analysis/pipeline_citations.bib, pipeline_sessionInfo.txt

## How to run it
Install R and RStudio, then open an R project in the folder that holds the .qmd file. The code uses here::here(), so paths are relative to the project root.
Install the packages the pipeline loads: clinicalsignificance, dplyr, effectsize, forcats, ggplot2, here, patchwork, psych, purrr, readr, readxl, rstatix, scales, stringr, tibble, tidyr and writexl. Stage 9 writes the definitive list to pipeline_citations.bib.
Create data/raw/ and place the three raw exports there with the file names in the table above.
Open surfwell_study2_pipeline.qmd and run the chunks in order, from stage 1 to stage 9.

Stage 5 is interactive. It pauses for a y/n answer after the outlier checks and after the test recommendations, and it has a step where you edit an Excel file before continuing. Run stage 5 chunk by chunk from the R console. Rendering the whole document in one go stops at the first prompt, by design, because these checks are meant to be answered by a person looking at the plots.

## Analytic choices
Multiple-testing correction is Bonferroni, applied within four hypothesis groups (Mental health, Wellbeing, Behaviour, Workplace performance). Days Surfing per Month and Intention to Leave are exploratory and are not corrected.
Three-timepoint measures use a repeated-measures ANOVA or a Friedman test, chosen from normality checks that include a researcher confirmation step. Post-hoc comparisons run only when the omnibus test is significant.
RCI uses the Jacobson-Truax method through the clinicalsignificance package. Intention to Leave and HPQ Absenteeism are not in the RCI.
Stage 4c is the single source of measure groups, display order, titles and axis labels.

The explanation for each decision sits beside the code it applies to, in the .qmd.

Contact

[Nick Knowles, Public Health and Sports Science, University of Exeter, nk366@exeter.ac.uk]
