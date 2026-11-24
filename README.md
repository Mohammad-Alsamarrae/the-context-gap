# The Context Gap

**What blind people need to know from a photo, and when they don’t get it.**

Data Science course project by **Mohammad Qasim Khalaf Alsamarrae**.

## The idea

Blind people use AI tools to understand what is in front of them: they take a photo and ask a question. But a description is not always enough. Hearing “a can” does not help someone who already knows it is a can by touch, and needs to know what is inside it, or where they are.

I call this the **context gap**: the difference between what the person is told about the object and the place around it, and what they actually need.

## The data

I built one table by merging three public datasets from the [VizWiz](https://vizwiz.org) project (validation split):

| Dataset | What it gives |
|---|---|
| VizWiz-VQA | A photo and a question from a blind user, with 10 answers from sighted volunteers |
| VizWiz-QualityIssues | Photo problems (blur, darkness, framing…) judged by 5 workers |
| VizWiz-Captions | 5 human descriptions of each photo |

On top of them I added my own features and target. The final table has **4,319 questions**, each linked to all three datasets.

The data is not stored in this repository: notebook 1 downloads it from the official VizWiz servers.

## The notebooks

Run them **in order** in Google Colab. In Colab every notebook runs on its own machine, so the files one notebook makes must be moved to the next by hand: download them from the folder icon on the left, and upload them in the next notebook. Notebook 3 asks for `clean_data.csv` if it cannot find it.

1. `notebooks/1_Data_Collection.ipynb`: downloads and loads the three datasets, checks that they link together
2. `notebooks/2_Data_Cleaning.ipynb`: cleans and merges everything into `clean_data.csv`
3. `notebooks/3_Features_and_Target.ipynb`: builds the features and the context gap target, saves `features_full.csv` and `analysis_table.csv`

Libraries: pandas, numpy and matplotlib.

## First results

- **49.8%** of questions have a context gap, even though every answer came from sighted people (38.8% with a lenient definition).
- The gap is highest for **reading text (66.7%)** and **scene or place questions (65.1%)**, and lowest for **color (19.0%)**.
- For reading questions, the descriptions said there is text but not what it says in **65.5%** of cases.
- Photos with **visibility problems** (blur, darkness) went unanswered far more often (**47%**) than photos with **framing problems** (cut, covered, rotated: **29%**).

## The reports

Every decision and its reason are written in the reports in `reports/`:

- `0_Preliminary_Report.pdf`: the idea and the plan
- `2_Data_Cleaning_Report.pdf`: all cleaning decisions
- `3_Features_and_Target_Report.pdf`: the features, the target and the first results

## Limits

- The answers come from human volunteers, not from an AI tool. Comparing AI answers on the same photos is a next step.
- The question types, description coverage and place mentions come from keyword rules, which can make mistakes.
- The data is in English and comes from VizWiz users.

## Next steps

- Phase 4: analyse how question type, photo problems and descriptions relate to the context gap.
- The intended use: a layer on top of an existing AI model that warns before a weak photo is sent, asks the model for the details that matter, and says clearly when it cannot read something. Its first answer should be as general as the question (the object and its place), and the person then chooses which detail to explore.

## Data credit

VizWiz datasets by the VizWiz team: [vizwiz.org](https://vizwiz.org). See their website for the terms of use.
