# Movie_Recommendation_System
Summer of Codes

Week-1

1. Data Loading and Preparation
File Used: tmdb_5000_movies.csv
Purpose: This dataset contains rich metadata for around 5,000 movies, including details like genres, budget, revenue, popularity, and more.
Action: You loaded the CSV into a pandas DataFrame for analysis.

2. Genre Data Extraction
Challenge: The genres column contains genre information in a JSON-like string format (e.g., [{"id": 18, "name": "Drama"}, ...]).
Solution: You used the ast.literal_eval function to safely convert these strings into Python lists of dictionaries, then extracted the genre names for each movie.
Result: You created a new column genre_names with the extracted genre names as lists.

3. Genre Analysis
Explode Genres: You used explode() to transform each movie’s list of genres into separate rows, so each genre is counted individually for movies that belong to multiple genres.
Count Genres: You counted the number of movies per genre using value_counts().

4. Visualization
Plot: You generated a bar chart (histogram) showing the number of movies per genre.
Purpose: This visualization helps identify which genres are most and least common in the dataset.

5. Key Insights
Genre Popularity: The bar chart reveals which genres dominate the dataset and which are less represented.
Data Quality: You handled the JSON-like genre data effectively, ensuring accurate counting and visualization.
Scalability: The approach works for large datasets and can be extended to other categorical data.

Week-2

1. Data Loading
Datasets Used:
movies_metadata.csv (main movie metadata)
keywords.csv (movie keywords)
links.csv (movie ID mappings)
credits.csv (movie cast and crew information)
Method:
Each dataset is loaded into a pandas DataFrame for manipulation and analysis.

2. Data Standardization and Cleaning
Standardizing IDs:
All relevant ID columns (id in movies, keywords, credits; tmdbId in links) are converted to strings and stripped of whitespace to ensure matching accuracy.
Removing Duplicates:
Duplicate entries are removed from each DataFrame based on their unique identifiers.

3. Merging Datasets
Base Dataset:
The movies DataFrame is used as the base to preserve all original movie records (46,628 rows before cleaning).
Left Joins:
Additional information from keywords, credits, and links is merged onto the base dataset using left joins, ensuring no movie is lost during merging.
Column Management:
After merging, unwanted columns (tmdbId, movieId, imdbId) are dropped to keep only relevant information.

4. Final Dataset
Shape and Columns:
The final merged DataFrame has 45,436 rows and 27 columns.
Columns include:
adult, belongs_to_collection, budget, genres, homepage, id, imdb_id, original_language, original_title, overview, popularity, poster_path, production_companies, production_countries, release_date, revenue, runtime, spoken_languages, status, tagline, title, video, vote_average, vote_count, keywords, cast, crew.
Saving:
The merged dataset is saved as master_dataset.csv.

Week-3

1. Data Loading and Initial Inspection
File Used: master_dataset.csv
Dataset Shape: The dataset contains 46,628 rows and 27 columns, as confirmed by the output: (46628, 27).
Purpose: This dataset serves as your master dataset for movie metadata and related information.

2. Data Preprocessing and Conversion
JSON/String Conversion: Columns such as cast, crew, and keywords were stored as strings (originally JSON-like). You converted these to Python lists using ast.literal_eval for easier manipulation.
Cast Processing: You extracted the top 3 cast members for each movie and converted their names to lowercase with spaces removed for consistency.
Keywords Processing: You extracted keywords, ensured they were in list form, and applied similar lowercase and space-removal transformations.
Director Extraction: You wrote a function to extract the director's name from the crew column and added it as a new column.

3. Feature Engineering
Keyword Analysis: You stacked all keywords to analyze their frequency, revealing the most common keywords (e.g., "woman director", "independent film", "murder", etc.).
Stemming: You applied stemming to keywords using the SnowballStemmer to normalize terms and reduce variations.
Feature Combination: You combined keywords, cast, director, and genres into a single "soup" column, joining all features as a space-separated string for each movie.

4. Data Quality and Consistency
List Conversion: You ensured that all relevant columns (keywords, cast, director, genres) are stored as lists, even if empty, to maintain consistency.
Uniqueness and Consistency: You removed spaces and converted names to lowercase to ensure uniformity and avoid duplication issues.

5. Saving the Processed Dataset
Output File: You saved the processed dataset as master_dataset_new.csv for use in further analysis or modeling.

Week-4 

1. Dataset Overview and Initial Processing
File Used: master_dataset_new.csv
Columns: The dataset originally contained a comprehensive set of movie features, including metadata (title, release date, popularity), cast, crew, keywords, genres, and derived features like "soup" (a combined text feature for recommendation).
Initial Steps: You loaded the CSV into a pandas DataFrame and inspected its columns to understand the available features.

2. Feature Selection and Cleaning
Unwanted Features Removed: You dropped several columns that were deemed unnecessary for your current analysis or recommendation system. This included metadata like budget, revenue, runtime, status, tagline, overview, and others, streamlining the dataset for focused analysis.
Data Type and Quality Checks:
Popularity: You ensured the popularity column contained only float values, removing rows with invalid data.
Director: You checked that the main director column contained valid strings, removing rows with empty or invalid entries.
Release Date: You verified the release date column for valid string entries, removing rows with missing or malformed dates.

3. Sorting and Filtering
Sorting by Popularity: You sorted the dataset by popularity in descending order to prioritize highly popular movies.
Top-N Selection: For demonstration or resource efficiency, you selected the top 2,500 movies from the sorted list.
Index Reset: After sorting and filtering, you reset the DataFrame index to maintain a clean and continuous index.

4. Final Dataset Structure
Remaining Columns: After cleaning and filtering, your dataset retained only the most relevant columns:
release_date
title
main_director
soup (a combined feature for content-based recommendation)
Purpose: This streamlined dataset is now ready for use in building or demonstrating a content-based movie recommendation system, focusing on the most popular movies and relevant features.

5. Key Techniques and Skills Learned
Data Cleaning: You learned how to identify and remove irrelevant or problematic data, ensuring the dataset is clean and reliable.
Feature Engineering: You gained experience in combining features (such as keywords, cast, genres) into a single "soup" feature for recommendation.
Data Type Handling: You practiced checking and enforcing data types (float for popularity, string for director and release date).
Sorting and Filtering: You learned to sort data by a specific metric (popularity) and select top rows for focused analysis or demonstration.
Index Management: You reset the DataFrame index after sorting and filtering to maintain data integrity.
