# DataScienceExercise
Purpose of this exercise is download the dataset, save it to a database and answer few questions.
<br />
Dataset source : <link>https://files.grouplens.org/datasets/movielens/ml-latest-small.zip</link>
<br />
### Data
This dataset (ml-latest-small) describes 5-star rating and free-text tagging activity from [MovieLens](http://movielens.org), a movie recommendation service. It contains 100836 ratings and 3683 tag applications across 9742 movies. These data were created by 610 users between March 29, 1996 and September 24, 2018. This dataset was generated on September 26, 2018.
<br /><br />
The data are contained in the files `links.csv`, `movies.csv`, `ratings.csv` and `tags.csv`.
<br />
For more information <link>https://grouplens.org/datasets/movielens/latest/</link>
### Question to be answered : 
1. How many movies are in data set ?
2. What is the most common genre of movie?
3. What are top 10 movies with highest rate ?
4. What are 5 most often rating users ?
5. When was done first and last rate included in data set and what was the rated movie tittle?
6. Find all movies released in 1990
### Two different solutions for the same questions
There are 2 main files in the SRC folder. One uses panda which provides better interfaces. Other one purely uses SqlAlchemy.
### Docker
To run the example, you can use the commands below.
<br />
#### Creating a new docker network
To be make sure all containers are in the same network, we should create a custome bridge network.
```console
docker network create datascienceExerciseHuseyin -d bridge
```
#### MySql container
To store the data in a specialized container, let's create a mysql container. In command below, we also set root users password.
```console
docker run --detach --name mysql --network "datascienceExerciseHuseyin" -p 3306:3306 -e MYSQL_ROOT_PASSWORD=password mysql
```
#### Analytics container
Finally let's set a container for running our code. For this exercise, we will use Jupyter-Notebook. Command below will install `pandas`, `sqlalchemy`, and `pymysql` packadges and clones the repository for convenience.
```console
docker run --name analytics -i -t --network "datascienceExerciseHuseyin" -p  8888:8888 continuumio/miniconda3 /bin/bash -c "/opt/conda/bin/conda install jupyter -y --quiet && mkdir -p /opt/notebooks && pip install pandas sqlalchemy pymysql && git clone https://github.com/HuseyinUtkuASLAN/DataScienceExercise.git /opt/notebooks && /opt/conda/bin/jupyter notebook --notebook-dir=/opt/notebooks --ip='*' --port=8888 --no-browser --allow-root"
```
### Current status of the project
Project is doing what it suppose to do and nothing more. All the questions are answered in main(pure_pandas).ipynb. For clean graphics, I used pandas. All the operations and selections are made in memory.
### Todo:
1. Prepare a decent docker compose.
