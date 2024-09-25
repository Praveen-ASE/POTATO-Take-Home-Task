Part 1: Ingesting the data

To ingest the data, I will use Python with the pandas library to read the TSV files and store the data in a structured format. I will use the larger 500MB file for this exercise.

import pandas as pd

# Read the larger TSV file

tweets_df = pd.read_csv('https://drive.google.com/uc?id=1cJf2GP2EIkX2jEWXHzIJaP25g9sw8dIT', sep='\t')

# Print the first few rows of the dataframe

print(tweets_df.head())

Part 2: Constructing functionality to query the data

To construct functionality to query the data, I will create a Python class that provides methods to answer the required questions.

class TweetAnalyzer:

      def __init__(self, tweets_df):
        self.tweets_df = tweets_df

     def get_tweets_per_day(self, term):
        # Filter tweets containing the term

        term_tweets = self.tweets_df[self.tweets_df['text'].str.contains(term, case=False)]

        # Group by day and count tweets
        tweets_per_day =
 term_tweets.groupby('created_at').size().reset_index(name='count')
        return tweets_per_day

    def get_unique_users(self, term):
        # Filter tweets containing the term

        term_tweets = self.tweets_df[self.tweets_df['text'].str.contains(term, case=False)]
        # Get unique users
        unique_users = term_tweets['user_id'].nunique()
        return unique_users

    def get_avg_likes(self, term):

        # Filter tweets containing the term
        term_tweets = self.tweets_df[self.tweets_df['text'].str.contains(term, case=False)]
        # Calculate average likes
        avg_likes = term_tweets['likes'].mean()
        return avg_likes

    def get_places(self, term):

        # Filter tweets containing the term
        term_tweets = self.tweets_df[self.tweets_df['text'].str.contains(term, case=False)]
        # Get places
        places = term_tweets['place_id'].value_counts().index.tolist()
        return places

    def get_times_of_day(self, term):
        # Filter tweets containing the term

        term_tweets = self.tweets_df[self.tweets_df['text'].str.contains(term, case=False)]
        # Get times of day
        times_of_day = term_tweets['created_at'].dt.hour.value_counts().index.tolist()
        return times_of_day

    def get_top_user(self, term):

        # Filter tweets containing the term
        term_tweets = self.tweets_df[self.tweets_df['text'].str.contains(term, case=False)]
        # Get top user
        top_user = term_tweets['user_id'].value_counts().index[0]
        return top_user 

        
Part 3 

To use this system, you can follow these steps:

Download the TSV file from the Google Drive link.
Run the code in Part 1 to ingest the data into a Pandas dataframe.
Create an instance of the TweetAnalyzer class, passing the dataframe as an argument.
Call the methods of the TweetAnalyzer class to query the data, such as get_tweets_per_day, get_unique_users, etc.

# Create an instance of the TweetAnalyzer class
analyzer = TweetAnalyzer(tweets_df)

# Query the data
tweets_per_day = analyzer.get_tweets_per_day('music')
print(tweets_per_day)

unique_users = analyzer.get_unique_users('music')
print(unique_users)

avg_likes = analyzer.get_avg_likes('music')
print(avg_likes)

places = analyzer.get_places('music')
print(places)

times_of_day = analyzer.get_times_of_day('music')
print(times_of_day)

top_user = analyzer.get_top_user('music')
print(top_user)




