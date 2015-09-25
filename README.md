Example request:

```
FROM_DATE=`date --date='2 weeks ago' '+%Y-%m-%d'`
curl -u <user>:<token> -G "https://api.github.com/search/issues" \
    --data-urlencode "q=user:aodn type:pr is:merged closed:>${FROM_DATE}" \
    --data-urlencode "sort=updated" \
    --data-urlencode "per_page=100" > prs.json

```


Pipe the output of the above to [jq](https://stedolan.github.io/jq), with a filter to extract the "summary" information:

```
$ curl ... | jq '[.items[] | {title: .title, user: .user.login, url: .html_url, body: .body, updated_at: .updated_at }]'
```

Open PRs:

curl -G "https://api.github.com/search/issues"        --data-urlencode "q=user:aodn type:pr is:open" --data-urlencode "sort=updated" --data-urlencode "order=asc" > open_prs.json



curl -u jkburges:`cat TOKEN` -G "https://api.github.com/search/issues" --data-urlencode "per_page=100"        --data-urlencode "q=user:aodn type:pr is:merged closed:>${FROM_DATE}" --data-urlencode "sort=updated" | jq '[.items[] | {title, url: .html_url, user: .user.login, updated_at, body}] ' > release_notes.json
