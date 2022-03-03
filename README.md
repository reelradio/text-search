# scraper

This tool is used to scrape a page and dump the contents into a MySQL table, called `tsearch`.

## To create the `tsearch` table

The file `create_tsearch.sql` is used to create the table.

In MySQL, run

```sql
\. create_tsearch.sql
```

to create the table.

## To scrape a page

Run

```
./scraper url
```

where `url` is points to the page you want to add to the table.
This inserts a line in the `insert_tsearch.sql` file. 
Once the `insert_tsearch.sql` file is fully populated, run

```sql
\. insert_tsearch.sql
```

in MySQL to insert all rows into the `tsearch` table.

## To scrape multiple pages

```
./file_scraper filename
```

where `filename` is a text file that contains a list of URLs that you want to scrape. Each URL must be separated by a new line.

## Running a query

The `tsearch` table is setup with a full text index, so instead of using the `LIKE` keyword in MySQL, we can use `MATCH` and `AGAINST`.
For example,

```sql
SELECT url
FROM tsearch
WHERE
    MATCH(body)
    AGAINST('query goes here');
```

