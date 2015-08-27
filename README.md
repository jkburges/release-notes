Example request:

```
FROM_DATE=`date --date='2 weeks ago' '+%Y-%m-%d'`
curl -G "https://api.github.com/search/issues"        --data-urlencode "q=user:aodn type:pr is:merged closed:>${FROM_DATE}" --data-urlencode "sort=updated" > prs.json

```


Pipe the output of the above to [jq](https://stedolan.github.io/jq), with a filter to extract the "summary" information:

```
$ curl ... | jq '.items | .[] |= with_entries(select(.key == ("title", "html_url", "body", "updated_at")))'
```

Open PRs:

curl -G "https://api.github.com/search/issues"        --data-urlencode "q=user:aodn type:pr is:open" --data-urlencode "sort=updated" --data-urlencode "order=asc" > open_prs.json
