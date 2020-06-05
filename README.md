# **Data Cleaning with PySpark live session**<br/>by **Mike Metzger**

Live training sessions are designed to mimic the flow of how a real data scientist would address a problem or a task. As such, a session needs to have some “narrative” where learners are achieving stated learning objectives in the form of a real-life data science task or project. For example, a data visualization live session could be around analyzing a dataset and creating a report with a specific business objective in mind _(ex: analyzing and visualizing churn)_, a data cleaning live session could be about preparing a dataset for analysis etc ... 

As part of the 'Live training Spec' process, you will need to complete the following tasks:

Edit this README by filling in the information for steps 1 - 4.

## Step 1: Foundations 

This part of the 'Live training Spec' process is designed to help guide you through session design by having you think through several key questions. Please make sure to delete the examples provided here for you.

### A. What problem(s) will students learn how to solve? (minimum of 5 problems)

- Reminders of lazy loading & Spark transformations vs actions
- Handling scenarios with improper data content (column counts, etc)
- Splitting column based on content
- Joining mutliple dataframes together
- Working with `monotonically_increasing_id`
- Using various functions from `pyspark.sql.functions` for data cleaning
- Using UDFs to clean data entries


### B. What technologies, packages, or functions will students use? Please be exhaustive.

- Spark
- Python

### C. What terms or jargon will you define?

- Spark Schemas: Much like a relational database schema, Spark dataframes have a schema or description of the columns and the types of data contained within.
- Parquet: A storage mechanism used in "big data", where data is stored in column format, allowing for easy query and access.

### D. What mistakes or misconceptions do you expect? 

- Remembering the various options available to load CSV data: There are a significant number of options available. Remembering the difference between options like `sep`, `quote`, etc can cause problems if the learner is not used to having documentation available (ie, Spark docs).

- Understanding that almost everything in Spark is done lazily: Nothing in Spark is actually executed until you run an action, such as `df.count()`, `df.write()`, etc. This can be difficult to troubleshoot if you're not certain what is happening.

### E. What datasets will you use? 

Netflix Movie dataset, custom "dirtied"

## Step 2: Who is this session for?

Terms like "beginner" and "expert" mean different things to different people, so we use personas to help instructors clarify a live training's audience. When designing a specific live training, instructors should explain how it will or won't help these people, and what extra skills or prerequisite knowledge they are assuming their students have above and beyond what's included in the persona.

- [ ] Please select the roles and industries that align with your live training. 
- [ ] Include an explanation describing your reasoning and any other relevant information. 

### What roles would this live training be suitable for?

*Check all that apply.*

- [ ] Data Consumer
- [ ] Leader 
- [x] Data Analyst
- [ ] Citizen Data Scientist
- [x] Data Scientist
- [x] Data Engineer
- [ ] Database Administrator
- [ ] Statistician
- [ ] Machine Learning Scientist
- [ ] Programmer
- [ ] Other (please describe)

Typically using Spark for data cleaning means you have to a) have a fair amount of data, b) understand that it needs to be cleaned / filtered / etc and what that means, and c) have something you intend to do with it afterwards. 

- Data Engineers often perform these steps. 
- Data Scientists may need to clean the data, or provide the list of things that should be cleaned. Understanding what is possible can assist with said list.
- Data Analysts would be on the cusp for this course, but might have input as a consumer of the data regarding what tasks to perform. 

### What industries would this apply to?

Generally, any industry in need of processing a lot of data where Spark is appropriate would qualify. Specifically, we're looking at batch style processing to clean data to prep for storage or analysis. 

### What level of expertise should learners have before beginning the live training?

*List three or more examples of skills that you expect learners to have before beginning the live training*

- Can load a Spark dataframe with data via CSV
- Understands general python usage, including imports and creation of functions
- Would have enough data to need a Spark solution and has a general idea what this means
- Has some knowledge of writing SQL / SQL style queries

## Step 3: Prerequisites

- Intro to PySpark
- Cleaning Data with PySpark

## Step 4: Session Outline

A live training session usually begins with an introductory presentation, followed by the live training itself, and an ending presentation. Your live session is expected to be around 2h30m-3h long (including Q&A) with a hard-limit at 3h30m. You can check out our live training content guidelines [here](_LINK_). 

### Introduction Slides
- Intro to the webinar and instructor
- Intro to the topics
  - Define data cleaning
  - Discuss reasons for using Spark and Python for data cleaning
  - Illustrate data set and some of the issues loading the data
  - Review session outline & describe Q&A process
  
### Live Training
#### Spark initialization and load DataFrame
- Import necessary Spark libraries and Colab helper tools
- Print our initial data source, illustrating the various problems with it (multiple column counts, odd separators, misformatted columns, etc)
- Try loading file(s) into Spark DataFrame using `spark.load.csv()`
- Show current schema using `.printSchema()`
- Reload file(s) into new Spark DataFrame using `spark.load.csv()` but with custom separator
- `.printSchema()` again, illustrating a single column DataFrame
- ** Q&A **

#### Initial Data Cleaning steps
- Use `.filter()` to remove any comment rows (multiple types of columns)
- Create a new column using `.withColumn()` with a count of our intended columns
- Use `.filter()` to remove any rows differing from the intended column count
- Determine the difference between current DataFrame and original to save off malformed data rows
- ** Q&A **

#### More Data Cleaning & Formatting
- Now split the remaining source data into actual DataFrame columns using combination of `.split()`, `.explode()`
- Use `.withColumnRenamed()` to rename columns to a usable format
- Create a UDF to split a string
- Apply the UDF to a combined name field
- Use `.drop()` to remove any unnecessary columns
- Add an id field using `.withColumn()` and `pyspark.sql.functions.monotonically_increasing_id()`
- Review the schema and save out to a Parquet file

#### End slides
- Recap
- Course suggestions


## Authoring your session

To get yourself started with setting up your live session, follow the steps below:

1. Download and install the "Open in Colabs" extension from [here](https://chrome.google.com/webstore/detail/open-in-colab/iogfkhleblhcpcekbiedikdehleodpjo?hl=en). This will let you take any jupyter notebook you see in a GitHub repository and open it as a **temporary** Colabs link.
2. Upload your dataset(s) to the `data` folder.
3. Upload your images, gifs, or any other assets you want to use in the notebook in the `assets` folder.
4. Check out the notebooks templates in the `notebooks` folder, and keep the template you want for your session while deleting all remaining ones.
5. Preview your desired notebook, press on "Open in Colabs" extension - and start developing your content in colabs _(which will act as the solution code to the session)_.  :warning: **Important** :warning: Your progress will **not** be saved on Google Colabs since it's a temporary link. To save your progress, make sure to press on `File`, `Save a copy in GitHub` and follow remaining prompts. You can also download the notebook locally and develop the content there as long you test out that the syntax works on Colabs as well.
6. Once your notebooks is ready to go, give it the name `session_name_solution.ipynb` create an empty version of the Notebook to be filled out by you and learners during the session, end the file name with `session_name_learners.ipynb`. 
7. Create Colabs links for both sessions and save them in notebooks :tada: 
