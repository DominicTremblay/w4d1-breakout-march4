-- Get the movies released after 2015

```sql
SELECT title, release_year
FROM movies
WHERE release_year > 2015;

```

-- List actors from the us

```sql
SELECT *
FROM actors
INNER JOIN countries
ON countries.id = actors.country_id
WHERE countries.name = 'United-States';
```

-- List movies with their director

```sql
SELECT movies.title, movies.director_id, directors.id, directors.first_name, directors.last_name
FROM movies
INNER JOIN directors
ON directors.id = movies.director_id;

```

-- List the movies with the genre 'adventure' or 'drama'

```sql
SELECT DISTINCT movies.title, movies.release_year, genres.description
FROM movies
INNER JOIN movie_genres
ON movies.id = movie_genres.movie_id
INNER JOIN genres
ON genres.id = movie_genres.genre_id
-- WHERE genres.description = 'Adventure' OR genres.description = 'Drama' OR genres.description = 'Thriller';
WHERE genres.description IN ('Adventure','Drama','Thriller');

```

-- If we want only the title of the movie wihout duplication

```sql
SELECT DISTINCT movies.title, movies.release_year
FROM movies
INNER JOIN movie_genres
ON movies.id = movie_genres.movie_id
INNER JOIN genres
ON genres.id = movie_genres.genre_id
-- WHERE genres.description = 'Adventure' OR genres.description = 'Drama' OR genres.description = 'Thriller';
WHERE genres.description IN ('Adventure','Drama','Thriller');
```

-- List all the actors even if they were not in a movie

```sql
SELECT actors.first_name, actors.last_name, movies.title FROM actors
LEFT OUTER JOIN actor_movies
ON actors.id = actor_movies.actor_id
LEFT OUTER JOIN movies
ON movies.id = actor_movies.movie_id;
```

-- List nb of movies per genre

```sql
SELECT genres.description, count(movie_genres.movie_id)
FROM genres
INNER JOIN movie_genres
ON genres.id = movie_genres.genre_id
GROUP BY genres.description;
```

-- List nb of movies per genre if more than 1 in DESC order

```sql
SELECT genres.description, count(movie_genres.movie_id) As movie_count
FROM genres
INNER JOIN movie_genres
ON genres.id = movie_genres.genre_id
GROUP BY genres.description
HAVING count(movie_genres.movie_id) > 1
ORDER BY count(movie_genres.movie_id) DESC;
```
