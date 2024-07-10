
## Project Report Template

> This repository serves as a template for your project reports as part of the Document Analysis lecture. To set up your project report as a webpage using GitHub Pages, simply follow the steps outlined in the next chapter.
>
>**Some Organizational Details:** Get creative with your project ideas! Just make sure they relate to Natural Language Processing and incorporate this specified dataset: [Link to data](https://huggingface.co/datasets/webis/tldr-17), [Link to paper](https://aclanthology.org/W17-4508.pdf). Submissions should be made in teams of 2-3 students. Each team is expected to create a blog-style project website, using GitHub Pages, to present their findings. Additionally, teams will deliver a lightning talk during the final lecture to discuss their project. Add all your code, such as Python scripts and Jupyter notebooks, to the `code` folder. Use markdown files for your project report. [Here](https://docs.gitlab.com/ee/user/markdown.html) you can read about how to format Markdown documents. 
>
>Have fun working on your project! 🥳

## Setup The Report Template

Follow this steps to set up your project report:

1. **Fork the Repository:** Begin by creating a copy of this repository for your own use. Click the `Fork` button at the top right corner of this page to do this.

2. **Configure GitHub Pages:** Navigate to `Settings` -> `Pages` in your newly forked repository. Under the `Branch` section, change from `None` to `master` and then click `Save`.

3. **Customize Configuration:** Modify the `_config.yml` file within your repository to personalize your site. Update the `title:` to reflect the title of your project and adjust the `description:` to provide a brief summary.

4. **Start Writing:** Start writing your report by modifying the `README.md`. You can also add new Markdown files for additional pages by modifying the `_config.yml` file. Use the standard [GitHub Markdown syntax](https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax) for formatting. 

5. **Access Your Site:** Return to `Settings` -> `Pages` in your repository to find the URL to your live site. It typically takes a few minutes for GitHub Pages to build and publish your site after updates. The URL to access your live site follows this schema: `https://<<username>>.github.io/<<repository_name>>/`

***

# Reddit Topic Telescope

Group members: Oksana Kalytenko, Mariia Pyvovar, Alisea Stroligo

## Introduction

[Start off by setting the stage for your project. Give a brief overview of relevant studies or work that have tackled similar issues. Then, clearly describe the main question or problem your project is designed to solve.]

This project analyses topics in the “ExplainLikeImFive” subreddit to understand community interests and sentiments through topic extraction and sentiment evaluation. It then combines findings from the previous two text-analysis techniques (Topic Modeling and Sentiment Analysis) to infer also non-textual properties of the dataset (e.g. general behaviors of users online).

## Dataset

[Provide a short description of the dataset used in your project. Focus on highlighting the aspects that are particularly relevant to your work.]

The dataset used for analyses consists of a corpus containing preprocessed posts from the Reddit dataset (Webis-TLDR-17), available at https://huggingface.co/datasets/webis/tldr-17. From this dataset, after preprocessing, for all further analyses (Topic Modeling, Sentiment Analysis and Network Analysis) only a subset of the data was used, i.e., all content from subreddit 'explainlikeimfive'. 
This particular subreddit was chosen due to content (we expected a variety of different topics mentioned in this particular subreddit, optimal for Topic Modeling), size (after preprocessing, this subreddit appeared among the 20 most visited subreddits, but not among the first ten, so that it provided a large amount of content but would also not be among the most computationally expensive for analyses) and finally it presented similar characteristics to other subreddits in terms of number of posts, number of authors and frequency of posts per author (i.e. important features for Network Analysis), therefore this subreddit also seemed to be a representative sample for the whole original dataset.
The complete data from the subreddit 'explainlikeimfive' can be found in a .zip file in the code folder of our GitHub repository.

## Methods

### Setup 


[Outline the tools, software, and hardware environment, along with configurations used for conducting your experiments. Be sure to document the Python version and other dependencies clearly. Provide step-by-step instructions on how to recreate your environment, ensuring anyone can replicate your setup with ease:

```bash
conda create --name myenv python=<version>
conda activate myenv
```

Include a `requirements.txt` file in your project repository. This file should list all the Python libraries and their versions needed to run the project. Provide instructions on how to install these dependencies using pip, for example:

```bash
pip install -r requirements.txt
```
]

Topic Modeling Setup  

Sentiment Analysis Setup  

Network Analysis Setup__  
software:__   
hardware environment: Microsoft Windows Version 22H2 (OS Build 19045.4529)__  
Python version: Python 3.9.13__    

To install Python libraries with the correct version run the following command in the terminal:
pip install -r requirements.txt  

### Experiments

[Report how you conducted the experiments. We suggest including detailed explanations of the preprocessing steps and model training in your project. For the preprocessing, describe  data cleaning, normalization, or transformation steps you applied to prepare the dataset, along with the reasons for choosing these methods. In the section on model training, explain the methodologies and algorithms you used, detail the parameter settings and training protocols, and describe any measures taken to ensure the validity of the models.]

## Results and Discussion

[Present the findings from your experiments, supported by visual or statistical evidence. Discuss how these results address your main research question.]

## Conclusion

[Summarize the major outcomes of your project, reflect on the research findings, and clearly state the conclusions you've drawn from the study.]

## Contributions

| Team Member  | Contributions                                             |
|--------------|-----------------------------------------------------------|
| Oksana Kalytenko | Data Preprocessing, Topic Modeling, Dashboard Creation&Design|                                                       |
| Mariia Pyvovar  | Data Preprocessing, Sentiment Analysis                                                       |
| Alisea Stroligo       | Data Preprocessing, Network Analysis                                                    |

## References

[Include a list of academic and professional sources you cited in your report, using an appropriate citation format to ensure clarity and proper attribution.]

