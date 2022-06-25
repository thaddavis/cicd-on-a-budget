# STEP

- https://git-scm.com/book/en/v2/Customizing-Git-Git-Hooks
- https://www.atlassian.com/git/tutorials/git-hooks
- https://medium.com/weekly-webtips/
- how-to-create-and-run-git-hooks-d395ec60d0d

# STEP

- create post-merge file
- must make hook file executable - `chmod +x post-merge`

- tested succesfully with
```
git co -b feature/testing # // git co feature/testing
git add -A
git ci -m "test"
git co main
git merge feature/testing
```

# STEP

https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html

- added `aws --version` to post-merge script
- added `npm -v` to post-merge script
- added `node -v` to post-merge script

# STEP

added
```
branch=$(git symbolic-ref HEAD | sed -e "s/^refs\/heads\///");

echo Current branch is: $branch

if [ "main" == "$branch" ]; then
    npm install
    npm run export
    aws s3 rm --recursive s3://$BUCKET_NAME
    aws s3 sync ./out s3://$BUCKET_NAME
    echo 'INVALIDATING CLOUDFRONT DISTRIBUTION'
    res=$(aws cloudfront create-invalidation --distribution-id $CLOUDFRONT_DISTRO_ID --paths "/*")
    echo 'UPDATE DEPLOYED'
fi
```

Needed to add IAM user role

# STEP

And that's all folks!!!


