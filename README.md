# WP CLI Snippets
_Make life easier with dope WP CLI commands._

### Move posts to new sub directory
A very common need is to move posts that have been written with the permalink setting `/%postname%/` to something like `/blog/%postname%/`. I've seen all types of solutions but I wanted a quick one liner to make this happen fast. This command was written specifically with the [Redirection](https://wordpress.org/plugins/redirection/) plugin in mind, which supports the import of csv files.

```
echo "source URL,target URL" > posts.csv; wp post list --post_type=post --post_status=publish --posts_per_page=-1 --fields=post_name --format=csv | sed '/post_name/d' | sed 's/\(.*\)/\/\1\/,\/blog\/\1\//g' >> posts.csv; wp redirection import posts.csv --format=csv;
```

The outcome of this should be a new file named `posts.csv`
